---
title: "aaaUsing système pour la gestion d’identité entre domaines déployez automatiquement des utilisateurs et des groupes à partir d’Azure Active Directory tooapplications | Documents Microsoft"
description: "Azure Active Directory peuvent automatiquement approvisionner les utilisateurs et groupes tooany application ou identité banque qui est fronted par un service web avec l’interface hello défini dans la spécification du protocole SCIM de hello"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="0bb0a-103">À l’aide du système pour configurer les utilisateurs tooautomatically de gestion des identités entre domaines et les groupes à partir d’Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="0bb0a-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="0bb0a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0bb0a-104">Overview</span></span>
<span data-ttu-id="0bb0a-105">Azure Active Directory (Azure AD) peuvent automatiquement approvisionner les utilisateurs et groupes tooany application ou identité banque qui est fronted par un service web avec l’interface hello défini dans hello [système pour inter-domaines Identity Management (SCIM) 2.0 spécification du protocole](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="0bb0a-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="0bb0a-106">Azure Active Directory peut envoyer des demandes toocreate, modifier ou supprimer des utilisateurs et groupes toohello web service affecté.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="0bb0a-107">service web de Hello peut traduire ces demandes en opérations sur le magasin d’identités cible hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0bb0a-108">Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="0bb0a-109">![][0]
*Figure 1 : Configuration de magasin d’identités Azure Active Directory tooan via un service web*</span><span class="sxs-lookup"><span data-stu-id="0bb0a-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="0bb0a-110">Cette fonctionnalité peut être utilisée conjointement avec la fonctionnalité de « apportez votre propre application » hello dans Azure AD tooenable l’authentification unique et de configuration pour les applications qui fournissent ou sont fronted par un service web SCIM automatique de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="0bb0a-111">Il existe deux cas d’utilisation de SCIM dans Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="0bb0a-112">**Approvisionnement tooapplications utilisateurs et groupes qui prennent en charge SCIM** Applications qui prennent en charge SCIM 2.0 et utilisent des jetons de porteur OAuth pour l’authentification fonctionne avec Azure AD sans configuration.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="0bb0a-113">**Créer votre propre solution d’approvisionnement pour les applications qui prennent en charge d’autres la configuration basée sur les API** pour les applications non-SCIM, vous pouvez créer un tootranslate de point de terminaison SCIM entre le point de terminaison Azure AD SCIM hello et toute application prend en charge API hello pour la configuration de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="0bb0a-114">toohelp vous développez un point de terminaison SCIM, nous fournissons des bibliothèques du Common Language Infrastructure (CLI), ainsi que des exemples de code qui montrent comment toodo fournissent un point de terminaison SCIM et traduire les messages de SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="0bb0a-115">Configuration des utilisateurs et groupes tooapplications qui prennent en charge SCIM</span><span class="sxs-lookup"><span data-stu-id="0bb0a-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="0bb0a-116">Azure AD peut être tooapplications d’utilisateurs et groupes de disposition affectée tooautomatically configuré qui implémentent un [système pour la gestion d’identité entre domaines 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) service web et d’accepter des jetons de porteur OAuth pour l’authentification .</span><span class="sxs-lookup"><span data-stu-id="0bb0a-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="0bb0a-117">Dans la spécification de hello SCIM 2.0, applications doivent respecter ces conditions :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="0bb0a-118">Prend en charge la création d’utilisateurs ou des groupes, conformément à la section 3.3 de hello protocole SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="0bb0a-119">Prend en charge la modification des utilisateurs ou des groupes avec des demandes de correctif logiciel conformément à la section 3.5.2 Hello protocole SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="0bb0a-120">Prend en charge la récupération d’une ressource connue en fonction de la section 3.4.1 Hello protocole SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="0bb0a-121">Prend en charge l’interrogation des utilisateurs ou des groupes, conformément à la section 3.4.2 Hello protocole SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="0bb0a-122">Par défaut, les utilisateurs sont interrogés par externalId et les groupes sont interrogés par displayName.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="0bb0a-123">Prend en charge l’interrogation d’utilisateur, par ID, par le gestionnaire conformément à la section 3.4.2 Hello protocole SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="0bb0a-124">Prend en charge l’interrogation des groupes par ID et par membre conformément à la section 3.4.2 Hello protocole SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="0bb0a-125">Accepte les jetons de porteur OAuth pour l’autorisation conformément à la section 2.1 du protocole SCIM de hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="0bb0a-126">Vérifiez avec votre fournisseur d’application ou dans la documentation du fournisseur de votre application la conformité à ces exigences.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="0bb0a-127">Prise en main</span><span class="sxs-lookup"><span data-stu-id="0bb0a-127">Getting started</span></span>
<span data-ttu-id="0bb0a-128">Les applications qui prennent en charge le profil SCIM hello décrite dans cet article peuvent être connecté tooAzure Active Directory à l’aide de la fonctionnalité de hello « bibliothèque non application » dans la galerie d’applications hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="0bb0a-129">Une fois connecté, Azure AD s’exécute un processus de synchronisation toutes les 20 minutes où elle interroge le point de terminaison de l’application hello SCIM pour utilisateurs et groupes et crée ou modifie les selon toohello détails de l’affectation.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="0bb0a-130">**tooconnect une application qui prend en charge SCIM :**</span><span class="sxs-lookup"><span data-stu-id="0bb0a-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="0bb0a-131">Connectez-vous trop[hello Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bb0a-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="0bb0a-132">Parcourir trop ** Azure Active Directory > Applications d’entreprise, puis sélectionnez **nouvelle application > tous les > application Non-gallery**.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="0bb0a-133">Entrez un nom pour votre application, puis cliquez sur **ajouter** icône toocreate un objet application.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="0bb0a-134">![][1]
  *Figure 2 : galerie d’applications Azure AD*</span><span class="sxs-lookup"><span data-stu-id="0bb0a-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="0bb0a-135">Dans l’écran hello résultant, sélectionnez hello **Provisioning** onglet dans la colonne de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="0bb0a-136">Bonjour **Mode d’approvisionnement** menu, sélectionnez **automatique**.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="0bb0a-137">![][2]
  *Figure 3 : Configuration de l’approvisionnement Bonjour portail Azure*</span><span class="sxs-lookup"><span data-stu-id="0bb0a-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="0bb0a-138">Bonjour **URL de client** , entrez l’URL de hello du point de terminaison de l’application hello SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="0bb0a-139">Par exemple : https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="0bb0a-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="0bb0a-140">Si le point de terminaison hello SCIM requiert un jeton de support OAuth à partir d’un émetteur autre que Azure AD, puis hello de copie requis de jeton de support OAuth dans hello facultatif **Secret jeton** champ.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="0bb0a-141">Si ce champ est laissé vide, Azure AD inclut un jeton de porteur OAuth émis par Azure AD avec chaque requête.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="0bb0a-142">Les applications qui utilisent Azure AD comme fournisseur d’identité peuvent valider ce jeton émis par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="0bb0a-143">Cliquez sur hello **tester la connexion** bouton toohave Azure Active Directory tentative tooconnect toohello SCIM point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="0bb0a-144">Si hello tentatives échouent, les informations d’erreur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="0bb0a-145">Si hello tentatives tooconnect toohello application réussisse, puis cliquez sur **enregistrer** toosave l’identification d’administrateur d’hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="0bb0a-146">Bonjour **mappages** section, il existe deux ensembles sélectionnables des mappages d’attributs : un pour les objets utilisateur et un pour les objets de groupe.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="0bb0a-147">Sélectionnez chaque un tooreview hello des attributs qui sont synchronisés à partir de l’application de tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="0bb0a-148">Hello attributs sélectionnés en tant que **correspondance** propriétés sont utilisées toomatch hello utilisateurs et groupes dans votre application pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="0bb0a-149">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0bb0a-150">Vous pouvez éventuellement désactiver la synchronisation des objets de groupe en désactivant hello « groupes de » de mappage.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="0bb0a-151">Sous **paramètres**, hello **étendue** champ définit les utilisateurs et les groupes sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="0bb0a-152">En sélectionnant « Synchronisation uniquement affecté aux utilisateurs et groupes » (recommandé) est synchronisés uniquement les utilisateurs et groupes affectés Bonjour **utilisateurs et groupes** onglet.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="0bb0a-153">Une fois que votre configuration est terminée, modifiez hello **état d’approvisionnement** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="0bb0a-154">Cliquez sur **enregistrer** toostart hello service de configuration d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="0bb0a-155">Si la synchronisation uniquement affecté aux utilisateurs et groupes (recommandés), être vraiment tooselect hello **utilisateurs et groupes** onglet, puis attribuez les utilisateurs de hello et/ou groupes que vous souhaitez toosync.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="0bb0a-156">Une fois la synchronisation initiale hello a démarré, vous pouvez utiliser hello **journaux d’Audit** onglet progression toomonitor, qui affiche toutes les actions effectuées par hello mise en service du service sur votre application.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="0bb0a-157">Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="0bb0a-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="0bb0a-158">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="0bb0a-159">Création de votre propre solution d’attribution pour n’importe quelle application</span><span class="sxs-lookup"><span data-stu-id="0bb0a-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="0bb0a-160">En créant un service Web SCIM doté d'une interface avec Azure Active Directory, vous pouvez activer l'authentification unique et l'attribution d'utilisateurs d'automatique pour pratiquement n'importe quelle application qui fournit une API d'attribution d'utilisateurs REST ou SOAP.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="0bb0a-161">Fonctionnement :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-161">Here’s how it works:</span></span>

1. <span data-ttu-id="0bb0a-162">Azure AD fournit une bibliothèque Common Language Infrastructure nommée [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="0bb0a-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="0bb0a-163">Les développeurs et les intégrateurs système toocreate de cette bibliothèque et de déployer un site web SCIM point de terminaison capable de se connecter de magasin d’identités de l’application Azure AD tooany.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="0bb0a-164">Les mappages sont implémentées dans hello web service toomap hello standardisé utilisateur toohello utilisateur schéma et de protocole requis par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="0bb0a-165">URL de point de terminaison Hello est inscrit dans Azure AD en tant que partie d’une application personnalisée dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="0bb0a-166">Utilisateurs et groupes bénéficient d’application toothis dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="0bb0a-167">Lors de l’affectation, ils sont placés dans une application cible de file d’attente toobe synchronisé toohello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="0bb0a-168">le processus de synchronisation gère la file d’attente hello Hello s’exécute toutes les 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="0bb0a-169">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="0bb0a-169">Code Samples</span></span>
<span data-ttu-id="0bb0a-170">toomake ce processus, un ensemble de [exemples de code](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) sont fournis que créer un point de terminaison du service web SCIM et montrent la configuration automatique.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="0bb0a-171">Exemple : un fournisseur qui gère un fichier avec des lignes de valeurs séparées par des virgules représentant des utilisateurs et des groupes.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="0bb0a-172">Hello autres est d’un fournisseur qui fonctionne sur le service Amazon Web Services Gestion des identités et l’accès de hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="0bb0a-173">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="0bb0a-173">**Prerequisites**</span></span>

* <span data-ttu-id="0bb0a-174">Visual Studio 2013 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="0bb0a-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="0bb0a-175">Kit de développement logiciel (SDK) Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="0bb0a-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="0bb0a-176">Ordinateur Windows qui prend en charge hello ASP.NET framework 4.5 toobe sert hello de point de terminaison SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="0bb0a-177">Cet ordinateur doit être accessible à partir du cloud de hello</span><span class="sxs-lookup"><span data-stu-id="0bb0a-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="0bb0a-178">Dans un abonnement Azure avec une version d’évaluation ou sous licence d’Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="0bb0a-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="0bb0a-179">exemple d’Amazon AWS Hello requiert des bibliothèques à partir de hello [Toolkit AWS pour Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="0bb0a-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="0bb0a-180">Pour plus d’informations, consultez hello Lisez-moi fichier inclus dans l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="0bb0a-181">Mise en route</span><span class="sxs-lookup"><span data-stu-id="0bb0a-181">Getting Started</span></span>
<span data-ttu-id="0bb0a-182">Hello tooimplement de façon simple un point de terminaison SCIM qui peut accepter la mise en service des demandes d’Azure AD est toobuild et déployer l’exemple de code hello qui génère le fichier de valeurs séparées par des virgules (CSV) tooa hello utilisateurs fournis.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="0bb0a-183">**toocreate un point de terminaison SCIM exemple :**</span><span class="sxs-lookup"><span data-stu-id="0bb0a-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="0bb0a-184">Télécharger le package d’exemple de code hello à [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="0bb0a-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="0bb0a-185">Décompressez le package de hello et placez-le sur votre ordinateur Windows à un emplacement tel que C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="0bb0a-186">Dans ce dossier, lancez hello FileProvisioningAgent de solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="0bb0a-187">Sélectionnez **Outils > Gestionnaire de Package de bibliothèque > Package Manager Console**et exécutez hello suivant les commandes pour les références de solution du projet tooresolve hello hello FileProvisioningAgent :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="0bb0a-188">Générez le projet de FileProvisioningAgent hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="0bb0a-189">Lancer l’application d’invite de commandes hello dans Windows (en tant qu’administrateur) et utilisez hello **cd** commande toochange hello Active tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** dossier.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="0bb0a-190">Exécutez hello commande suivante, en remplaçant < adresse ip > avec hello IP adresse ou nom de domaine de l’ordinateur de Windows hello :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="0bb0a-191">Dans Windows sous **paramètres Windows > réseau et les paramètres Internet**, sélectionnez hello **pare-feu Windows > Paramètres avancés**et créer un **règle de trafic entrant** qui permet l’accès entrant tooport 9000.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="0bb0a-192">Si la machine virtuelle Windows hello est derrière un routeur, hello routeur besoins toobe configuré tooperform traduction d’accès réseau entre le port 9000 qui est exposé toohello internet et le port 9000 sur l’ordinateur de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="0bb0a-193">Cela est nécessaire pour tooaccess en mesure de Azure AD toobe ce point de terminaison dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="0bb0a-194">**tooregister hello exemple SCIM point de terminaison dans Azure AD :**</span><span class="sxs-lookup"><span data-stu-id="0bb0a-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="0bb0a-195">Connectez-vous trop[hello Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bb0a-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="0bb0a-196">Parcourir trop ** Azure Active Directory > Applications d’entreprise, puis sélectionnez **nouvelle application > tous les > application Non-gallery**.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="0bb0a-197">Entrez un nom pour votre application, puis cliquez sur **ajouter** icône toocreate un objet application.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="0bb0a-198">objet d’application Hello créé est prévue toorepresent hello cible application serait approvisionner tooand mise en œuvre de point de terminaison unique hello d’authentification pour et pas seulement SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="0bb0a-199">Dans l’écran hello résultant, sélectionnez hello **Provisioning** onglet dans la colonne de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="0bb0a-200">Bonjour **Mode d’approvisionnement** menu, sélectionnez **automatique**.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="0bb0a-201">![][2]
  *Figure 4 : Configuration de l’approvisionnement Bonjour portail Azure*</span><span class="sxs-lookup"><span data-stu-id="0bb0a-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="0bb0a-202">Bonjour **URL de client** , entrez l’URL de hello exposés à internet et de port de votre point de terminaison SCIM.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="0bb0a-203">Cela serait quelque chose comme http://testmachine.contoso.com:9000 ou http://<ip-address>:9000/, où < adresse ip > est hello internet exposées IP adresse.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="0bb0a-204">Si le point de terminaison hello SCIM requiert un jeton de support OAuth à partir d’un émetteur autre que Azure AD, puis hello de copie requis de jeton de support OAuth dans hello facultatif **Secret jeton** champ.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="0bb0a-205">Si ce champ est laissé vide, Azure AD inclura un jeton de porteur OAuth émis par Azure AD avec chaque requête.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="0bb0a-206">Les applications qui utilisent Azure AD comme fournisseur d’identité peuvent valider ce jeton émis par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="0bb0a-207">Cliquez sur hello **tester la connexion** bouton toohave Azure Active Directory tentative tooconnect toohello SCIM point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="0bb0a-208">Si hello tentatives échouent, les informations d’erreur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="0bb0a-209">Si hello tentatives tooconnect toohello application réussisse, puis cliquez sur **enregistrer** toosave l’identification d’administrateur d’hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="0bb0a-210">Bonjour **mappages** section, il existe deux ensembles sélectionnables des mappages d’attributs : un pour les objets utilisateur et un pour les objets de groupe.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="0bb0a-211">Sélectionnez chaque un tooreview hello des attributs qui sont synchronisés à partir de l’application de tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="0bb0a-212">Hello attributs sélectionnés en tant que **correspondance** propriétés sont utilisées toomatch hello utilisateurs et groupes dans votre application pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="0bb0a-213">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="0bb0a-214">Sous **paramètres**, hello **étendue** champ définit les utilisateurs et les groupes sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="0bb0a-215">En sélectionnant « Synchronisation uniquement affecté aux utilisateurs et groupes » (recommandé) est synchronisés uniquement les utilisateurs et groupes affectés Bonjour **utilisateurs et groupes** onglet.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="0bb0a-216">Une fois que votre configuration est terminée, modifiez hello **état d’approvisionnement** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="0bb0a-217">Cliquez sur **enregistrer** toostart hello service de configuration d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="0bb0a-218">Si la synchronisation uniquement affecté aux utilisateurs et groupes (recommandés), être vraiment tooselect hello **utilisateurs et groupes** onglet, puis attribuez les utilisateurs de hello et/ou groupes que vous souhaitez toosync.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="0bb0a-219">Une fois la synchronisation initiale hello a démarré, vous pouvez utiliser hello **journaux d’Audit** onglet progression toomonitor, qui affiche toutes les actions effectuées par hello mise en service du service sur votre application.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="0bb0a-220">Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="0bb0a-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="0bb0a-221">étape finale de Hello de vérification de l’exemple hello est tooopen hello fichier TargetFile.csv dans le dossier de \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello sur votre ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="0bb0a-222">Une fois que hello processus de déploiement est exécuté, ce fichier montre les détails hello de tous les affecté et configuré les utilisateurs et groupes.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="0bb0a-223">Bibliothèques de développement</span><span class="sxs-lookup"><span data-stu-id="0bb0a-223">Development libraries</span></span>
<span data-ttu-id="0bb0a-224">toodevelop votre propre service web qui est conforme à la spécification SCIM toohello, tout d’abord vous familiariser avec hello suivant bibliothèques fournies par Microsoft toohelp accélérer le processus de développement hello :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="0bb0a-225">Les bibliothèques CLI (Common Language Infrastructure) sont proposées pour une utilisation avec les langages basés sur cette infrastructure, notamment C#.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="0bb0a-226">Une de ces bibliothèques, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), déclare une interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, illustrée hello suivant illustration : A développeur à l’aide des bibliothèques de hello implémente cette interface avec une classe qui peut être appelée de façon générique, en tant que fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="0bb0a-227">les bibliothèques Hello activer hello développeur toodeploy un service web qui respecte la spécification de SCIM toohello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="0bb0a-228">service web de Hello peut être soit hébergé dans Internet Information Services, ou n’importe quel assembly du Common Language Infrastructure exécutable.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="0bb0a-229">Demande est traduite en, ces méthodes appels toohello fournisseur seraient être programmées par toooperate de développeur hello sur le magasin d’identités.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="0bb0a-230">[Express gestionnaires d’itinéraire](http://expressjs.com/guide/routing.html) sont disponibles pour l’analyse des objets de requête node.js représentant des appels (tel que défini par la spécification de SCIM de hello), service web de node.js tooa.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="0bb0a-231">Création d’un point de terminaison SCIM personnalisé</span><span class="sxs-lookup"><span data-stu-id="0bb0a-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="0bb0a-232">À l’aide des bibliothèques CLI hello, les développeurs qui utilisent ces bibliothèques peuvent héberger leurs services dans un assembly de Common Language Infrastructure exécutable, ou dans Internet Information Services.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="0bb0a-233">Voici un exemple de code pour l’hébergement d’un service dans un assembly exécutable, à l’adresse hello http://localhost : 9000 :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="0bb0a-234">Ce service doit avoir un HTTP adresse et serveur de certificat d’authentification de quels hello autorité de certification racine est hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="0bb0a-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="0bb0a-235">CNNIC</span></span>
* <span data-ttu-id="0bb0a-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="0bb0a-236">Comodo</span></span>
* <span data-ttu-id="0bb0a-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="0bb0a-237">CyberTrust</span></span>
* <span data-ttu-id="0bb0a-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="0bb0a-238">DigiCert</span></span>
* <span data-ttu-id="0bb0a-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="0bb0a-239">GeoTrust</span></span>
* <span data-ttu-id="0bb0a-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="0bb0a-240">GlobalSign</span></span>
* <span data-ttu-id="0bb0a-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="0bb0a-241">Go Daddy</span></span>
* <span data-ttu-id="0bb0a-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="0bb0a-242">Verisign</span></span>
* <span data-ttu-id="0bb0a-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="0bb0a-243">WoSign</span></span>

<span data-ttu-id="0bb0a-244">Un certificat d’authentification serveur peut être le port lié tooa sur un hôte Windows à l’aide de l’utilitaire shell hello réseau :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="0bb0a-245">Ici, la valeur hello fournie pour l’argument de certhash hello est l’empreinte numérique hello du certificat de hello, tandis que la valeur hello fournie pour l’argument d’appid hello est un identificateur global unique arbitraire.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="0bb0a-246">service de hello toohost dans Internet Information Services, un développeur serait générer un assembly de bibliothèque de code CLA avec une classe nommée démarrage dans l’espace de noms hello par défaut de l’assembly hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="0bb0a-247">Voici un exemple de classe de ce type :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="0bb0a-248">Gestion de l’authentification du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="0bb0a-248">Handling endpoint authentication</span></span>
<span data-ttu-id="0bb0a-249">Les demandes d’Azure Active Directory incluent un jeton de support OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="0bb0a-250">Toute demande hello réception de service doit authentifier émetteur hello comme étant Azure Active Directory pour le compte de locataire Azure Active Directory hello attendu, pour un accès toohello service web de Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="0bb0a-251">Jeton de hello, l’émetteur de hello est identifié par une revendication d’iss, comme « iss » : « https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/ ».</span><span class="sxs-lookup"><span data-stu-id="0bb0a-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="0bb0a-252">Dans cet exemple, l’adresse de base hello de valeur de revendication hello, https://sts.windows.net, identifie les Azure Active Directory comme hello émetteur, tandis que le segment de l’adresse relative, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello est un identificateur unique de hello Azure Active Locataire d’annuaire pour le compte qui hello jeton a été émis.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="0bb0a-253">Si le jeton de hello a été émis pour accéder au service web de Azure Active Directory Graph hello, puis identificateur hello de ce service, 00000002-0000-0000-c000-type "000000000000", doit être dans la valeur hello aud du jeton hello de revendication.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="0bb0a-254">Les développeurs qui utilisent les bibliothèques CLA hello fournies par Microsoft pour la création d’un service SCIM peuvent authentifier les demandes d’Azure Active Directory à l’aide de paquet Microsoft.owin.Security.ActiveDirectory hello en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="0bb0a-255">Dans un fournisseur, implémenter la propriété Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior de hello en le faisant retournent un toobe méthode appelée chaque fois que le service de hello est démarré :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="0bb0a-256">Ajoutez hello suivant code toothat méthode toohave tooany de toute demande de points de terminaison du service hello authentifié comme portant un jeton émis par Azure Active Directory pour le compte d’un client spécifié, pour l’accès toohello service web de Azure AD Graph :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="0bb0a-257">Schéma des utilisateurs et des groupes</span><span class="sxs-lookup"><span data-stu-id="0bb0a-257">User and group schema</span></span>
<span data-ttu-id="0bb0a-258">Azure Active Directory peuvent configurer deux types de ressources tooSCIM web services.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="0bb0a-259">Ces types de ressources sont des utilisateurs et des groupes.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="0bb0a-260">Ressources de l’utilisateur sont identifiés par l’identificateur de schéma hello, urn : ietf:params:scim:schemas:extension:enterprise:2.0:User, qui est inclus dans cette spécification de protocole : http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="0bb0a-261">mappage par défaut de Hello d’attributs hello d’utilisateurs dans les attributs de toohello Azure Active Directory des ressources de l’urn : ietf:params:scim:schemas:extension:enterprise:2.0:User est fourni dans le tableau 1, ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="0bb0a-262">Ressources du groupe sont identifiés par l’identificateur de schéma hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="0bb0a-263">Le tableau 2 ci-dessous montre hello par défaut mappés attributs hello des groupes dans Azure les attributs Active Directory toohello des ressources de http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="0bb0a-264">Tableau 1 : Mappage d’attributs utilisateur par défaut</span><span class="sxs-lookup"><span data-stu-id="0bb0a-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="0bb0a-265">Utilisateur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bb0a-265">Azure Active Directory user</span></span> | <span data-ttu-id="0bb0a-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="0bb0a-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="0bb0a-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="0bb0a-267">IsSoftDeleted</span></span> |<span data-ttu-id="0bb0a-268">active</span><span class="sxs-lookup"><span data-stu-id="0bb0a-268">active</span></span> |
| <span data-ttu-id="0bb0a-269">displayName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-269">displayName</span></span> |<span data-ttu-id="0bb0a-270">displayName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-270">displayName</span></span> |
| <span data-ttu-id="0bb0a-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="0bb0a-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="0bb0a-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="0bb0a-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="0bb0a-273">givenName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-273">givenName</span></span> |<span data-ttu-id="0bb0a-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-274">name.givenName</span></span> |
| <span data-ttu-id="0bb0a-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="0bb0a-275">jobTitle</span></span> |<span data-ttu-id="0bb0a-276">title</span><span class="sxs-lookup"><span data-stu-id="0bb0a-276">title</span></span> |
| <span data-ttu-id="0bb0a-277">mail</span><span class="sxs-lookup"><span data-stu-id="0bb0a-277">mail</span></span> |<span data-ttu-id="0bb0a-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="0bb0a-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="0bb0a-279">mailNickName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-279">mailNickname</span></span> |<span data-ttu-id="0bb0a-280">externalId</span><span class="sxs-lookup"><span data-stu-id="0bb0a-280">externalId</span></span> |
| <span data-ttu-id="0bb0a-281">manager</span><span class="sxs-lookup"><span data-stu-id="0bb0a-281">manager</span></span> |<span data-ttu-id="0bb0a-282">manager</span><span class="sxs-lookup"><span data-stu-id="0bb0a-282">manager</span></span> |
| <span data-ttu-id="0bb0a-283">mobile</span><span class="sxs-lookup"><span data-stu-id="0bb0a-283">mobile</span></span> |<span data-ttu-id="0bb0a-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="0bb0a-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="0bb0a-285">objectId</span><span class="sxs-lookup"><span data-stu-id="0bb0a-285">objectId</span></span> |<span data-ttu-id="0bb0a-286">id</span><span class="sxs-lookup"><span data-stu-id="0bb0a-286">id</span></span> |
| <span data-ttu-id="0bb0a-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="0bb0a-287">postalCode</span></span> |<span data-ttu-id="0bb0a-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="0bb0a-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="0bb0a-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="0bb0a-289">proxy-Addresses</span></span> |<span data-ttu-id="0bb0a-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="0bb0a-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="0bb0a-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="0bb0a-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="0bb0a-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="0bb0a-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="0bb0a-293">streetAddress</span></span> |<span data-ttu-id="0bb0a-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="0bb0a-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="0bb0a-295">surname</span><span class="sxs-lookup"><span data-stu-id="0bb0a-295">surname</span></span> |<span data-ttu-id="0bb0a-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-296">name.familyName</span></span> |
| <span data-ttu-id="0bb0a-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="0bb0a-297">telephone-Number</span></span> |<span data-ttu-id="0bb0a-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="0bb0a-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="0bb0a-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-299">user-PrincipalName</span></span> |<span data-ttu-id="0bb0a-300">userName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="0bb0a-301">Tableau 2 : Mappage d’attribut par défaut</span><span class="sxs-lookup"><span data-stu-id="0bb0a-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="0bb0a-302">Groupe Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bb0a-302">Azure Active Directory group</span></span> | <span data-ttu-id="0bb0a-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="0bb0a-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="0bb0a-304">displayName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-304">displayName</span></span> |<span data-ttu-id="0bb0a-305">externalId</span><span class="sxs-lookup"><span data-stu-id="0bb0a-305">externalId</span></span> |
| <span data-ttu-id="0bb0a-306">mail</span><span class="sxs-lookup"><span data-stu-id="0bb0a-306">mail</span></span> |<span data-ttu-id="0bb0a-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="0bb0a-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="0bb0a-308">mailNickName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-308">mailNickname</span></span> |<span data-ttu-id="0bb0a-309">displayName</span><span class="sxs-lookup"><span data-stu-id="0bb0a-309">displayName</span></span> |
| <span data-ttu-id="0bb0a-310">membres</span><span class="sxs-lookup"><span data-stu-id="0bb0a-310">members</span></span> |<span data-ttu-id="0bb0a-311">membres</span><span class="sxs-lookup"><span data-stu-id="0bb0a-311">members</span></span> |
| <span data-ttu-id="0bb0a-312">objectId</span><span class="sxs-lookup"><span data-stu-id="0bb0a-312">objectId</span></span> |<span data-ttu-id="0bb0a-313">id</span><span class="sxs-lookup"><span data-stu-id="0bb0a-313">id</span></span> |
| <span data-ttu-id="0bb0a-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="0bb0a-314">proxyAddresses</span></span> |<span data-ttu-id="0bb0a-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="0bb0a-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="0bb0a-316">Approvisionnement et annulation d’approvisionnement utilisateur</span><span class="sxs-lookup"><span data-stu-id="0bb0a-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="0bb0a-317">Hello après l’illustration montre les messages hello qu’Azure Active Directory envoie tooa SCIM service toomanage hello du cycle de vie d’un utilisateur dans un autre magasin d’identités.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="0bb0a-318">diagramme de Hello montre également comment un service SCIM implémenté à l’aide des bibliothèques CLI hello fourni par Microsoft pour la génération de que ces services traduire par ces demandes toohello appelle des méthodes d’un fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="0bb0a-319">![][4]
*Figure 5 : séquence d’approvisionnement et d’annulation de l’approvisionnement d’utilisateurs*</span><span class="sxs-lookup"><span data-stu-id="0bb0a-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="0bb0a-320">Les requêtes Active Directory Azure hello service pour un utilisateur avec une valeur d’attribut externalId correspondance la valeur de l’attribut mailNickname hello d’un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="0bb0a-321">requête de Hello est exprimée comme une demande de protocole HTTP (Hypertext Transfer) telles que cet exemple, dans lequel jyoung est un exemple d’un mailNickname d’un utilisateur dans Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="0bb0a-322">Si le service de hello a été généré à l’aide de bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduite dans un toohello d’appel de méthode de requête de fournisseur de service hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="0bb0a-323">Voici la signature hello de cette méthode :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-323">Here is hello signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="0bb0a-324">Voici la définition hello d’interface de Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="0bb0a-325">Bonjour suivant l’exemple d’une requête pour un utilisateur avec une valeur donnée pour l’attribut d’externalId hello, les valeurs des arguments hello passés la méthode de requête toohello sont :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="0bb0a-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="0bb0a-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="0bb0a-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="0bb0a-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="0bb0a-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="0bb0a-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="0bb0a-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="0bb0a-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="0bb0a-331">Si hello réponse tooa toohello service web de requêtes pour un utilisateur avec une valeur d’attribut externalId qui correspond à la valeur de l’attribut mailNickname hello d’un utilisateur ne renvoie pas de tous les utilisateurs, Azure Active Directory demande ensuite cette disposition de service hello un utilisateur toohello correspondant un dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="0bb0a-332">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="0bb0a-333">bibliothèques de Common Language Infrastructure Hello fournis par Microsoft pour l’implémentation de services SCIM traduit cette demande dans un toohello d’appel de méthode Create de fournisseur de service hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="0bb0a-334">Hello méthode Create a cette signature :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="0bb0a-335">Dans une demande tooprovision un utilisateur, valeur hello d’argument de ressource hello est une instance de hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="0bb0a-336">Classe de Core2EnterpriseUser, définie dans la bibliothèque de Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="0bb0a-337">Si l’utilisateur de hello tooprovision hello demande réussit, puis hello implémentation de méthode hello est attendu tooreturn une instance de hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="0bb0a-338">Classe Core2EnterpriseUser, avec la valeur hello de propriété de l’identificateur hello définie toohello d’identificateur unique de l’utilisateur qui vient d’être configuré de hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="0bb0a-339">tooupdate un utilisateur connu tooexist dans un magasin d’identités fronted par un SCIM, continue d’Azure Active Directory en demandant l’état actuel de hello de cet utilisateur à partir du service de hello avec une demande, tels que :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="0bb0a-340">Dans un service est généré à l’aide des bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduit en un toohello d’appel de méthode de récupération du fournisseur de service hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="0bb0a-341">Voici la signature hello de méthode de récupération hello :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-341">Here is hello signature of hello Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="0bb0a-342">Dans l’exemple hello d’un état demande tooretrieve hello en cours d’un utilisateur, les valeurs de hello des propriétés de hello d’objet hello fournie comme valeur de hello d’argument de paramètres hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="0bb0a-343">Identificateur "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="0bb0a-344">SchemaIdentifier : "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="0bb0a-345">Si un attribut de référence est toobe mis à jour, puis Azure Active Directory requêtes hello service toodetermine ou non hello valeur actuelle de l’attribut de référence hello dans le magasin d’identités hello fronted par service de hello correspond déjà la valeur hello de l’attribut dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="0bb0a-346">Pour les utilisateurs, hello seul attribut de quels hello valeur actuelle est interrogée de cette façon est hello manager.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="0bb0a-347">Voici un exemple d’une demande de toodetermine si l’attribut de gestionnaire hello d’un objet utilisateur particulier a actuellement une certaine valeur :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="0bb0a-348">Hello la valeur de paramètre de requête hello attributs id, signifie que s’il existe un objet utilisateur est conforme aux expression hello fournie en tant que valeur hello hello filtre du paramètre de requête, puis service de hello est toorespond attendu avec un urn : ietf:params:scim:schemas : ressource de noyaux : 2.0:User ou urn : ietf:params:scim:schemas:extension:enterprise:2.0:User, incluant hello uniquement la valeur d’attribut d’id de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="0bb0a-349">Hello valeur Hello **id** est inconnu toohello demandeur.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="0bb0a-350">Il est inclus dans la valeur hello hello filtre du paramètre de requête ; Hello lui demandant d’elle vise réellement toorequest une représentation minimale d’une ressource qui satisfont à expression de filtre hello comme une indication de ces ou non l’objet existe.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="0bb0a-351">Si le service de hello a été généré à l’aide de bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduite dans un toohello d’appel de méthode de requête de fournisseur de service hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="0bb0a-352">valeur de Hello de propriétés hello objet hello fournie comme valeur de hello d’argument de paramètres hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="0bb0a-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="0bb0a-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="0bb0a-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="0bb0a-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="0bb0a-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="0bb0a-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="0bb0a-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager</span><span class="sxs-lookup"><span data-stu-id="0bb0a-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="0bb0a-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="0bb0a-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="0bb0a-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="0bb0a-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="0bb0a-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="0bb0a-362">Ici, valeur hello de l’index hello x peut être 0 et valeur hello de hello index y peut être de 1, ou valeur hello de x peut-être être de 1 et valeur hello y peut être 0, selon l’ordre de hello des expressions de hello hello filtre du paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="0bb0a-363">Voici un exemple d’une demande à partir d’Azure Active Directory tooan SCIM service tooupdate un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="0bb0a-364">bibliothèques de Microsoft Common Language Infrastructure Hello pour l’implémentation de services SCIM traduit les demande hello dans un toohello d’appel de méthode de mise à jour du fournisseur de service hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="0bb0a-365">Voici la signature hello Hello méthode de mise à jour :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-365">Here is hello signature of hello Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="0bb0a-366">Dans l’exemple hello d’une demande de tooupdate un utilisateur, objet hello fournie comme valeur de hello d’argument de correctif hello possède ces valeurs de propriété :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="0bb0a-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="0bb0a-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="0bb0a-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="0bb0a-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="0bb0a-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="0bb0a-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="0bb0a-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="0bb0a-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="0bb0a-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="0bb0a-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="0bb0a-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="0bb0a-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="0bb0a-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="0bb0a-375">un utilisateur à partir d’un magasin d’identités de provisionnement toode fronted par un service SCIM, Azure AD envoie une demande de telles que :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="0bb0a-376">Si le service de hello a été généré à l’aide de bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduite dans un toohello d’appel de méthode de suppression du fournisseur de service hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="0bb0a-377">Cette méthode a sa signature :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="0bb0a-378">objet de Hello fournie comme valeur de hello d’argument de resourceIdentifier hello possède ces valeurs de propriété dans l’exemple hello d’une demande toode-disposition un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="0bb0a-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="0bb0a-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="0bb0a-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="0bb0a-381">Approvisionnement et annulation d’approvisionnement d’un groupe</span><span class="sxs-lookup"><span data-stu-id="0bb0a-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="0bb0a-382">Hello après l’illustration montre les messages hello que Azure AcD envoie tooa SCIM service toomanage hello du cycle de vie d’un groupe dans un autre magasin d’identités.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="0bb0a-383">Ces messages diffèrent des messages hello se rapportant toousers de trois façons :</span><span class="sxs-lookup"><span data-stu-id="0bb0a-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="0bb0a-384">schéma de Hello d’une ressource de groupe est identifié en tant que http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="0bb0a-385">Requêtes tooretrieve groupes stipulent cet attribut de membres hello est toobe exclu à partir de n’importe quelle ressource fournie dans la demande de toohello de réponse.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="0bb0a-386">Toodetermine demandes indique si un attribut de référence a une certaine valeur sont des requêtes sur les attributs des membres hello.</span><span class="sxs-lookup"><span data-stu-id="0bb0a-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="0bb0a-387">![][5]
*Figure 6 : séquence d’approvisionnement et d’annulation de l’approvisionnement d’un groupe*</span><span class="sxs-lookup"><span data-stu-id="0bb0a-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="0bb0a-388">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="0bb0a-388">Related articles</span></span>
* [<span data-ttu-id="0bb0a-389">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bb0a-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="0bb0a-390">Automatiser la configuration d’utilisateur/Deprovisioning tooSaaS applications</span><span class="sxs-lookup"><span data-stu-id="0bb0a-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="0bb0a-391">Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0bb0a-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="0bb0a-392">Écriture d’expressions pour les mappages d’attributs</span><span class="sxs-lookup"><span data-stu-id="0bb0a-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="0bb0a-393">Filtres d’étendue pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0bb0a-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="0bb0a-394">Notifications d’approvisionnement de comptes</span><span class="sxs-lookup"><span data-stu-id="0bb0a-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="0bb0a-395">Liste des didacticiels sur la façon de tooIntegrate applications SaaS</span><span class="sxs-lookup"><span data-stu-id="0bb0a-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
