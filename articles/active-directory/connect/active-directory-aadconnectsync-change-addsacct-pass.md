---
title: "Synchronisation Azure AD Connect : mot de passe du compte de service d’annuaire hello AD modification | Documents Microsoft"
description: "Document de cette rubrique décrit comment tooupdate Azure AD Connect après le mot de passe hello du compte de hello AD DS est modifiée."
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
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="edd66-104">Modification de mot de passe de compte hello AD DS</span><span class="sxs-lookup"><span data-stu-id="edd66-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="edd66-105">compte de Hello AD DS fait référence toohello compte d’utilisateur utilisé par toocommunicate Azure AD Connect avec Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="edd66-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="edd66-106">Si vous modifiez le mot de passe hello Hello compte AD DS, vous devez mettre à jour un Service Azure AD Connect synchronisation avec le nouveau mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="edd66-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="edd66-107">Dans le cas contraire, hello que la synchronisation peut ne plus synchroniser correctement avec hello Active Directory sur site et vous rencontrerez hello les erreurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="edd66-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="edd66-108">Bonjour opération Synchronization Service Manager, toute importation ou d’exportation avec local échoue AD avec **non-start-informations d’identification** erreur.</span><span class="sxs-lookup"><span data-stu-id="edd66-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="edd66-109">Dans l’Observateur d’événements Windows, journal des événements application hello contient une erreur avec **événement ID 6000** et message **'agent de gestion hello « contoso.com » a échoué toorun, car les informations d’identification hello n’étaient pas valides'** .</span><span class="sxs-lookup"><span data-stu-id="edd66-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="edd66-110">Comment tooupdate hello Service de synchronisation avec le nouveau mot de passe pour le compte de domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="edd66-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="edd66-111">tooupdate hello Service de synchronisation avec le nouveau mot de passe hello :</span><span class="sxs-lookup"><span data-stu-id="edd66-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="edd66-112">Démarrez hello Synchronization Service Manager (Service de synchronisation de début →).</span><span class="sxs-lookup"><span data-stu-id="edd66-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="edd66-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="edd66-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="edd66-114">Accédez toohello **connecteurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="edd66-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="edd66-115">Sélectionnez hello **Connecteur AD** qui correspond le compte de service d’annuaire toohello AD dont son mot de passe a été modifié.</span><span class="sxs-lookup"><span data-stu-id="edd66-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="edd66-116">Sous **Actions**, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="edd66-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="edd66-117">Dans la boîte de dialogue contextuelle hello, sélectionnez **connecter tooActive Directory forêt**:</span><span class="sxs-lookup"><span data-stu-id="edd66-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="edd66-118">Entrez hello nouveau mot de passe du compte de hello AD DS dans hello **mot de passe** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="edd66-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="edd66-119">Cliquez sur **OK** toosave hello nouveau mot de passe et de la boîte de dialogue contextuelle hello fermer.</span><span class="sxs-lookup"><span data-stu-id="edd66-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="edd66-120">Redémarrage hello Service Azure AD Connect synchronisation sous le Gestionnaire de contrôle de Service Windows.</span><span class="sxs-lookup"><span data-stu-id="edd66-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="edd66-121">Il s’agit de tooensure que toute référence toohello ancien mot de passe est supprimé du cache de mémoire hello.</span><span class="sxs-lookup"><span data-stu-id="edd66-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edd66-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="edd66-122">Next steps</span></span>
<span data-ttu-id="edd66-123">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="edd66-123">**Overview topics**</span></span>

* [<span data-ttu-id="edd66-124">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="edd66-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="edd66-125">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edd66-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
