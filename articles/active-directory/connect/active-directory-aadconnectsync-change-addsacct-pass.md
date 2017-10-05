---
title: "Synchronisation Azure AD Connect : modification de mot de passe de compte AD DS | Microsoft Docs"
description: "Cette rubrique décrit comment mettre à jour Azure AD Connect après la modification du mot de passe du compte AD DS."
services: active-directory
keywords: "Compte AD DS, compte Active Directory, mot de passe"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="49375-104">Modifier le mot de passe du compte AD DS</span><span class="sxs-lookup"><span data-stu-id="49375-104">Changing the AD DS account password</span></span>
<span data-ttu-id="49375-105">Le compte AD DS fait référence au compte d’utilisateur utilisé par Azure AD Connect pour communiquer avec le répertoire Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="49375-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="49375-106">Si vous modifiez le mot de passe du compte AD DS, vous devez mettre à jour le service de synchronisation Azure AD Connect avec le nouveau mot de passe.</span><span class="sxs-lookup"><span data-stu-id="49375-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="49375-107">Dans le cas contraire, la synchronisation avec le répertoire Active Directory local ne s’effectue plus correctement et les erreurs suivantes apparaissent :</span><span class="sxs-lookup"><span data-stu-id="49375-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="49375-108">Dans Synchronization Service Manager, toute opération d’importation ou d’exportation avec le répertoire local Active Directory échoue avec une erreur **no-start-credentials**.</span><span class="sxs-lookup"><span data-stu-id="49375-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="49375-109">Dans l’Observateur d’événements Windows, le journal d’événement d’application contient une erreur avec l’**ID d’événement 6000** et le message **«  failed to run because the credentials were invalid « contoso.com » en raison d'informations d'identification non valides. »**.</span><span class="sxs-lookup"><span data-stu-id="49375-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="49375-110">Mise à jour du service de synchronisation avec un nouveau mot de passe pour le compte AD DS</span><span class="sxs-lookup"><span data-stu-id="49375-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="49375-111">Pour mettre à jour le service de synchronisation avec le nouveau mot de passe :</span><span class="sxs-lookup"><span data-stu-id="49375-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="49375-112">Démarrez Synchronization Service Manager (DÉMARRER → Service de synchronisation).</span><span class="sxs-lookup"><span data-stu-id="49375-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="49375-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="49375-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="49375-114">Accédez à l’onglet **Connecteurs** .</span><span class="sxs-lookup"><span data-stu-id="49375-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="49375-115">Sélectionnez le **Connecteur AD** correspondant au compte AD DS dont le mot de passe a été modifié.</span><span class="sxs-lookup"><span data-stu-id="49375-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="49375-116">Sous **Actions**, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="49375-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="49375-117">Dans la boîte de dialogue contextuelle, sélectionnez **Se connecter à la forêt Active Directory** :</span><span class="sxs-lookup"><span data-stu-id="49375-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="49375-118">Dans la zone de texte **Mot de passe**, tapez le nouveau mot de passe du compte AD DS.</span><span class="sxs-lookup"><span data-stu-id="49375-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="49375-119">Cliquez sur **OK** pour enregistrer le nouveau mot de passe et fermez la boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="49375-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="49375-120">Redémarrez le service de synchronisation Azure AD Connect sous le Gestionnaire de contrôle des services Windows.</span><span class="sxs-lookup"><span data-stu-id="49375-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="49375-121">Cela permet de s’assurer que toute référence à l’ancien mot de passe est supprimée du cache mémoire.</span><span class="sxs-lookup"><span data-stu-id="49375-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49375-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49375-122">Next steps</span></span>
<span data-ttu-id="49375-123">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="49375-123">**Overview topics**</span></span>

* [<span data-ttu-id="49375-124">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="49375-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="49375-125">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49375-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
