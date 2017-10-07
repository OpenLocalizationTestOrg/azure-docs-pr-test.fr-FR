---
title: aaaConnectors Bonjour Azure Active Directory Synchronization Service Manager UI | Des documents Microsoft
description: "Comprendre l’onglet connecteurs hello hello Synchronization Service Manager pour Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="716df-103">À l’aide de connecteurs avec hello Azure AD Connect Sync Service Manager</span><span class="sxs-lookup"><span data-stu-id="716df-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="716df-105">onglet de connecteurs Hello est utilisé toomanage moteur de synchronisation de tous les systèmes hello est connecté à.</span><span class="sxs-lookup"><span data-stu-id="716df-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="716df-106">Actions du connecteur</span><span class="sxs-lookup"><span data-stu-id="716df-106">Connector actions</span></span>
| <span data-ttu-id="716df-107">Action</span><span class="sxs-lookup"><span data-stu-id="716df-107">Action</span></span> | <span data-ttu-id="716df-108">Commentaire</span><span class="sxs-lookup"><span data-stu-id="716df-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="716df-109">Créer</span><span class="sxs-lookup"><span data-stu-id="716df-109">Create</span></span> |<span data-ttu-id="716df-110">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="716df-110">Do not use.</span></span> <span data-ttu-id="716df-111">Pour vous connecter tooadditional AD forêts, utilisez l’Assistant installation hello.</span><span class="sxs-lookup"><span data-stu-id="716df-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="716df-112">Propriétés</span><span class="sxs-lookup"><span data-stu-id="716df-112">Properties</span></span> |<span data-ttu-id="716df-113">Permet le filtrage de domaine et d’unité organisationnelle.</span><span class="sxs-lookup"><span data-stu-id="716df-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="716df-114">Supprimer</span><span class="sxs-lookup"><span data-stu-id="716df-114">Delete</span></span>](#delete) |<span data-ttu-id="716df-115">Tooeither utilisé supprimer les données de hello dans la forêt par connecteur hello espace ou toodelete tooa de connexion.</span><span class="sxs-lookup"><span data-stu-id="716df-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="716df-116">Configurer les profils d’exécution</span><span class="sxs-lookup"><span data-stu-id="716df-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="716df-117">À l’exception de domaine, le filtrage, rien ne tooconfigure ici.</span><span class="sxs-lookup"><span data-stu-id="716df-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="716df-118">Vous pouvez utiliser cette action profils d’exécution toosee déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="716df-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="716df-119">Exécuter</span><span class="sxs-lookup"><span data-stu-id="716df-119">Run</span></span> |<span data-ttu-id="716df-120">Utilisé toostart One-Off exécution d’un profil.</span><span class="sxs-lookup"><span data-stu-id="716df-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="716df-121">Arrêter</span><span class="sxs-lookup"><span data-stu-id="716df-121">Stop</span></span> |<span data-ttu-id="716df-122">Arrête un connecteur qui exécute un profil.</span><span class="sxs-lookup"><span data-stu-id="716df-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="716df-123">Exporter le connecteur</span><span class="sxs-lookup"><span data-stu-id="716df-123">Export Connector</span></span> |<span data-ttu-id="716df-124">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="716df-124">Do not use.</span></span> |
| <span data-ttu-id="716df-125">Importer le connecteur</span><span class="sxs-lookup"><span data-stu-id="716df-125">Import Connector</span></span> |<span data-ttu-id="716df-126">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="716df-126">Do not use.</span></span> |
| <span data-ttu-id="716df-127">Mettre à jour le connecteur</span><span class="sxs-lookup"><span data-stu-id="716df-127">Update Connector</span></span> |<span data-ttu-id="716df-128">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="716df-128">Do not use.</span></span> |
| <span data-ttu-id="716df-129">Actualiser le schéma</span><span class="sxs-lookup"><span data-stu-id="716df-129">Refresh Schema</span></span> |<span data-ttu-id="716df-130">Actualise le schéma de mise en cache hello.</span><span class="sxs-lookup"><span data-stu-id="716df-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="716df-131">Il est préféré toouse hello dans l’Assistant installation Bonjour au lieu de cela, étant donné que les mises à jour synchronise aussi règles.</span><span class="sxs-lookup"><span data-stu-id="716df-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="716df-132">Espace de connecteur de recherche</span><span class="sxs-lookup"><span data-stu-id="716df-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="716df-133">Les objets de toofind utilisés et trop[suivre un objet et ses données via le système de hello](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="716df-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="716df-134">Supprimer</span><span class="sxs-lookup"><span data-stu-id="716df-134">Delete</span></span>
<span data-ttu-id="716df-135">action de suppression Hello est utilisée pour deux choses différentes.</span><span class="sxs-lookup"><span data-stu-id="716df-135">hello delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="716df-137">Hello option **suppression de l’espace de connecteur uniquement** supprime toutes les données, mais conserver hello configuration.</span><span class="sxs-lookup"><span data-stu-id="716df-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="716df-138">Hello option **supprimer le connecteur et le connecteur de l’espace** supprime les données de salutation et configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="716df-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="716df-139">Cette option est utilisée lorsque vous ne souhaitez pas plus tooconnect tooa forêt.</span><span class="sxs-lookup"><span data-stu-id="716df-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="716df-140">Les deux options de tous les objets de synchronisation et mettre à jour les objets du métaverse hello.</span><span class="sxs-lookup"><span data-stu-id="716df-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="716df-141">Cette action est une opération de longue durée.</span><span class="sxs-lookup"><span data-stu-id="716df-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="716df-142">Configurer les profils d’exécution</span><span class="sxs-lookup"><span data-stu-id="716df-142">Configure Run Profiles</span></span>
<span data-ttu-id="716df-143">Cette option vous permet de hello toosee profils configurés pour un connecteur d’exécution.</span><span class="sxs-lookup"><span data-stu-id="716df-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="716df-145">Espace de connecteur de recherche</span><span class="sxs-lookup"><span data-stu-id="716df-145">Search Connector Space</span></span>
<span data-ttu-id="716df-146">action d’espace connecteur Hello recherche des objets toofind utiles et résoudre les problèmes de données.</span><span class="sxs-lookup"><span data-stu-id="716df-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="716df-148">Commencez par sélectionner une **portée**.</span><span class="sxs-lookup"><span data-stu-id="716df-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="716df-149">Vous pouvez rechercher sur la base de données (RDN, le nom de domaine, d’ancrage, sous-arborescence), ou l’état de l’objet hello (toutes les autres options).</span><span class="sxs-lookup"><span data-stu-id="716df-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="716df-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="716df-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="716df-151">Par exemple, si vous effectuez une recherche dans la sous-arborescence, vous obtenez tous les objets d’une unité d’organisation.</span><span class="sxs-lookup"><span data-stu-id="716df-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="716df-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="716df-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="716df-153">À partir de cette grille, vous pouvez sélectionner un objet, sélectionnez **propriétés**, et [suivent](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) d’espace de connecteur source hello, via le métaverse hello et l’espace de connecteur toohello cible.</span><span class="sxs-lookup"><span data-stu-id="716df-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="716df-154">Modification de mot de passe de compte hello AD DS</span><span class="sxs-lookup"><span data-stu-id="716df-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="716df-155">Si vous modifiez le mot de passe de compte hello, hello Service de synchronisation ne pourra plus être en mesure de tooimport/exportation modifications tooon local AD.</span><span class="sxs-lookup"><span data-stu-id="716df-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="716df-156">Vous pouvez voir les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="716df-156">You may see hello following:</span></span>

- <span data-ttu-id="716df-157">étape d’importation/exportation Hello pour hello Connecteur AD échoue avec l’erreur de « non-start-informations d’identification ».</span><span class="sxs-lookup"><span data-stu-id="716df-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="716df-158">Dans l’Observateur d’événements Windows, journal des événements application hello contient une erreur avec l’événement ID 6000 et le message « hello toorun de l’agent « contoso.com » et échoué de la gestion, car les informations d’identification hello n’étaient pas valides. »</span><span class="sxs-lookup"><span data-stu-id="716df-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="716df-159">tooresolve hello émettre, compte d’utilisateur mise à jour hello AD DS utilisation hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="716df-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="716df-160">Démarrez hello Synchronization Service Manager (Service de synchronisation de début →).</span><span class="sxs-lookup"><span data-stu-id="716df-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="716df-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="716df-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="716df-162">Accédez toohello **connecteurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="716df-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="716df-163">Sélectionnez hello le connecteur Active Directory qui est configuré toouse hello compte AD DS.</span><span class="sxs-lookup"><span data-stu-id="716df-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="716df-164">Sous Actions, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="716df-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="716df-165">Dans la boîte de dialogue contextuelle hello, sélectionnez se connecter tooActive Directory forêt :</span><span class="sxs-lookup"><span data-stu-id="716df-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="716df-166">nom de la forêt Hello indique hello correspondant locale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="716df-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="716df-167">nom d’utilisateur Hello indique le compte de service d’annuaire hello AD utilisé pour la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="716df-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="716df-168">Entrez hello nouveau mot de passe du compte de hello AD DS dans la zone de texte de mot de passe hello ![Azure AD connecter synchronisation chiffrement clé utilitaire](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="716df-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="716df-169">Cliquez sur OK toosave hello nouveau mot de passe et redémarrez hello Service de synchronisation tooremove hello ancien mot de passe à partir de la mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="716df-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="716df-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="716df-170">Next steps</span></span>
<span data-ttu-id="716df-171">En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="716df-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="716df-172">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="716df-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
