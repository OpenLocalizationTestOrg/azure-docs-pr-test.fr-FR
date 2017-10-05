---
title: "Connecteurs dans l’interface utilisateur d’Azure AD Synchronization Service Manager | Microsoft Docs"
description: "Comprendre l’onglet Connecteurs dans Synchronization Service Manager pour Azure AD Connect."
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
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="89e74-103">Utilisation de connecteurs avec Azure AD Connect Sync Service Manager</span><span class="sxs-lookup"><span data-stu-id="89e74-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="89e74-105">L’onglet Connecteurs permet de gérer tous les systèmes auquel le moteur de synchronisation est connecté.</span><span class="sxs-lookup"><span data-stu-id="89e74-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="89e74-106">Actions du connecteur</span><span class="sxs-lookup"><span data-stu-id="89e74-106">Connector actions</span></span>
| <span data-ttu-id="89e74-107">Action</span><span class="sxs-lookup"><span data-stu-id="89e74-107">Action</span></span> | <span data-ttu-id="89e74-108">Commentaire</span><span class="sxs-lookup"><span data-stu-id="89e74-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="89e74-109">Créer</span><span class="sxs-lookup"><span data-stu-id="89e74-109">Create</span></span> |<span data-ttu-id="89e74-110">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="89e74-110">Do not use.</span></span> <span data-ttu-id="89e74-111">Pour la connexion à des forêts Active Directory supplémentaires, utilisez l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="89e74-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="89e74-112">Propriétés</span><span class="sxs-lookup"><span data-stu-id="89e74-112">Properties</span></span> |<span data-ttu-id="89e74-113">Permet le filtrage de domaine et d’unité organisationnelle.</span><span class="sxs-lookup"><span data-stu-id="89e74-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="89e74-114">Supprimer</span><span class="sxs-lookup"><span data-stu-id="89e74-114">Delete</span></span>](#delete) |<span data-ttu-id="89e74-115">Permet de supprimer les données dans l’espace connecteur ou de supprimer la connexion à une forêt.</span><span class="sxs-lookup"><span data-stu-id="89e74-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="89e74-116">Configurer les profils d’exécution</span><span class="sxs-lookup"><span data-stu-id="89e74-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="89e74-117">À l’exception du filtrage de domaine, il n’y a rien à configurer ici.</span><span class="sxs-lookup"><span data-stu-id="89e74-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="89e74-118">Vous pouvez vous servir de cette action pour voir les profils d’exécution déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="89e74-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="89e74-119">Exécuter</span><span class="sxs-lookup"><span data-stu-id="89e74-119">Run</span></span> |<span data-ttu-id="89e74-120">Permet de lancer l’exécution unique d’un profil.</span><span class="sxs-lookup"><span data-stu-id="89e74-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="89e74-121">Arrêter</span><span class="sxs-lookup"><span data-stu-id="89e74-121">Stop</span></span> |<span data-ttu-id="89e74-122">Arrête un connecteur qui exécute un profil.</span><span class="sxs-lookup"><span data-stu-id="89e74-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="89e74-123">Exporter le connecteur</span><span class="sxs-lookup"><span data-stu-id="89e74-123">Export Connector</span></span> |<span data-ttu-id="89e74-124">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="89e74-124">Do not use.</span></span> |
| <span data-ttu-id="89e74-125">Importer le connecteur</span><span class="sxs-lookup"><span data-stu-id="89e74-125">Import Connector</span></span> |<span data-ttu-id="89e74-126">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="89e74-126">Do not use.</span></span> |
| <span data-ttu-id="89e74-127">Mettre à jour le connecteur</span><span class="sxs-lookup"><span data-stu-id="89e74-127">Update Connector</span></span> |<span data-ttu-id="89e74-128">Ne pas utiliser.</span><span class="sxs-lookup"><span data-stu-id="89e74-128">Do not use.</span></span> |
| <span data-ttu-id="89e74-129">Actualiser le schéma</span><span class="sxs-lookup"><span data-stu-id="89e74-129">Refresh Schema</span></span> |<span data-ttu-id="89e74-130">Actualise le schéma mis en cache.</span><span class="sxs-lookup"><span data-stu-id="89e74-130">Refreshes the cached schema.</span></span> <span data-ttu-id="89e74-131">Il est préférable d’utiliser l’option dans l’Assistant Installation, car les règles de synchronisation sont également mises à jour.</span><span class="sxs-lookup"><span data-stu-id="89e74-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="89e74-132">Espace de connecteur de recherche</span><span class="sxs-lookup"><span data-stu-id="89e74-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="89e74-133">Permet de rechercher des objets et de [Suivre un objet et ses données dans le système](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="89e74-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="89e74-134">Supprimer</span><span class="sxs-lookup"><span data-stu-id="89e74-134">Delete</span></span>
<span data-ttu-id="89e74-135">L’action de suppression est utilisée dans deux cas.</span><span class="sxs-lookup"><span data-stu-id="89e74-135">The delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="89e74-137">L’option **Supprimer l’espace connecteur uniquement** supprime toutes les données en conservant la configuration.</span><span class="sxs-lookup"><span data-stu-id="89e74-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="89e74-138">L’option **Supprimer le connecteur et l’espace connecteur** supprime les données et la configuration.</span><span class="sxs-lookup"><span data-stu-id="89e74-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="89e74-139">Utilisez cette option quand vous ne souhaitez plus vous connecter à une forêt.</span><span class="sxs-lookup"><span data-stu-id="89e74-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="89e74-140">Les deux options synchronisent tous les objets et mettent à jour les objets du métaverse.</span><span class="sxs-lookup"><span data-stu-id="89e74-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="89e74-141">Cette action est une opération de longue durée.</span><span class="sxs-lookup"><span data-stu-id="89e74-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="89e74-142">Configurer les profils d’exécution</span><span class="sxs-lookup"><span data-stu-id="89e74-142">Configure Run Profiles</span></span>
<span data-ttu-id="89e74-143">Cette option vous permet de voir les profils d'exécution configurées pour un connecteur.</span><span class="sxs-lookup"><span data-stu-id="89e74-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="89e74-145">Espace de connecteur de recherche</span><span class="sxs-lookup"><span data-stu-id="89e74-145">Search Connector Space</span></span>
<span data-ttu-id="89e74-146">L’action de recherche dans l’espace connecteur permet de rechercher des objets et de résoudre les problèmes relatifs aux données.</span><span class="sxs-lookup"><span data-stu-id="89e74-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="89e74-148">Commencez par sélectionner une **portée**.</span><span class="sxs-lookup"><span data-stu-id="89e74-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="89e74-149">Vous pouvez rechercher des données (nom unique relatif, nom de domaine, ancre, sous-arborescence) ou l’état de l’objet (toutes les autres options).</span><span class="sxs-lookup"><span data-stu-id="89e74-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="89e74-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="89e74-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="89e74-151">Par exemple, si vous effectuez une recherche dans la sous-arborescence, vous obtenez tous les objets d’une unité d’organisation.</span><span class="sxs-lookup"><span data-stu-id="89e74-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="89e74-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="89e74-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="89e74-153">À partir de cette grille, vous pouvez sélectionner un objet, sélectionner des **propriétés** et [les suivre](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) par le biais du métaverse, de l’espace connecteur source vers l’espace connecteur cible.</span><span class="sxs-lookup"><span data-stu-id="89e74-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="89e74-154">Modifier le mot de passe du compte AD DS</span><span class="sxs-lookup"><span data-stu-id="89e74-154">Changing the AD DS account password</span></span>
<span data-ttu-id="89e74-155">Si vous modifiez le mot de passe du compte, le service de synchronisation ne peut plus importer/exporter des modifications vers le répertoire Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="89e74-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="89e74-156">Le message suivant peut apparaître :</span><span class="sxs-lookup"><span data-stu-id="89e74-156">You may see the following:</span></span>

- <span data-ttu-id="89e74-157">L’étape d’importation/exportation pour le connecteur AD échoue avec l’erreur « no-start-credentials ».</span><span class="sxs-lookup"><span data-stu-id="89e74-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="89e74-158">Dans l’Observateur d’événements Windows, le journal d’événement d’application contient une erreur avec l’ID d’événement 6000 et le message « Échec de l'exécution de l'agent de gestion « contoso.com » en raison d'informations d'identification non valides ».</span><span class="sxs-lookup"><span data-stu-id="89e74-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="89e74-159">Pour résoudre ce problème, mettez à jour le compte d’utilisateur AD DS en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e74-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="89e74-160">Démarrez Synchronization Service Manager (DÉMARRER → Service de synchronisation).</span><span class="sxs-lookup"><span data-stu-id="89e74-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="89e74-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="89e74-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="89e74-162">Accédez à l’onglet **Connecteurs** .</span><span class="sxs-lookup"><span data-stu-id="89e74-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="89e74-163">Sélectionnez le connecteur Active Directory configuré pour utiliser le compte AD DS.</span><span class="sxs-lookup"><span data-stu-id="89e74-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="89e74-164">Sous Actions, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="89e74-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="89e74-165">Dans la boîte de dialogue contextuelle, sélectionnez Se connecter à la forêt Active Directory :</span><span class="sxs-lookup"><span data-stu-id="89e74-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="89e74-166">Le nom de la forêt indique le répertoire Active Directory local correspondant.</span><span class="sxs-lookup"><span data-stu-id="89e74-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="89e74-167">Le nom d’utilisateur indique le compte AD DS utilisé pour la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="89e74-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="89e74-168">Entrez le nouveau mot de passe du compte AD DS dans la zone de texte Mot de passe ![Utilitaire de clé de chiffrement Azure AD Connect Sync](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="89e74-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="89e74-169">Cliquez sur OK pour enregistrer le nouveau mot de passe et redémarrez le service de synchronisation pour supprimer l’ancien mot de passe du cache mémoire.</span><span class="sxs-lookup"><span data-stu-id="89e74-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="89e74-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89e74-170">Next steps</span></span>
<span data-ttu-id="89e74-171">En savoir plus sur la configuration de la [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="89e74-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="89e74-172">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="89e74-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
