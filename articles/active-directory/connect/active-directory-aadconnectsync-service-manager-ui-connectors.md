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
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>À l’aide de connecteurs avec hello Azure AD Connect Sync Service Manager

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

onglet de connecteurs Hello est utilisé toomanage moteur de synchronisation de tous les systèmes hello est connecté à.

## <a name="connector-actions"></a>Actions du connecteur
| Action | Commentaire |
| --- | --- |
| Créer |Ne pas utiliser. Pour vous connecter tooadditional AD forêts, utilisez l’Assistant installation hello. |
| Propriétés |Permet le filtrage de domaine et d’unité organisationnelle. |
| [Supprimer](#delete) |Tooeither utilisé supprimer les données de hello dans la forêt par connecteur hello espace ou toodelete tooa de connexion. |
| [Configurer les profils d’exécution](#configure-run-profiles) |À l’exception de domaine, le filtrage, rien ne tooconfigure ici. Vous pouvez utiliser cette action profils d’exécution toosee déjà configuré. |
| Exécuter |Utilisé toostart One-Off exécution d’un profil. |
| Arrêter |Arrête un connecteur qui exécute un profil. |
| Exporter le connecteur |Ne pas utiliser. |
| Importer le connecteur |Ne pas utiliser. |
| Mettre à jour le connecteur |Ne pas utiliser. |
| Actualiser le schéma |Actualise le schéma de mise en cache hello. Il est préféré toouse hello dans l’Assistant installation Bonjour au lieu de cela, étant donné que les mises à jour synchronise aussi règles. |
| [Espace de connecteur de recherche](#search-connector-space) |Les objets de toofind utilisés et trop[suivre un objet et ses données via le système de hello](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Supprimer
action de suppression Hello est utilisée pour deux choses différentes.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

Hello option **suppression de l’espace de connecteur uniquement** supprime toutes les données, mais conserver hello configuration.

Hello option **supprimer le connecteur et le connecteur de l’espace** supprime les données de salutation et configuration de hello. Cette option est utilisée lorsque vous ne souhaitez pas plus tooconnect tooa forêt.

Les deux options de tous les objets de synchronisation et mettre à jour les objets du métaverse hello. Cette action est une opération de longue durée.

### <a name="configure-run-profiles"></a>Configurer les profils d’exécution
Cette option vous permet de hello toosee profils configurés pour un connecteur d’exécution.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Espace de connecteur de recherche
action d’espace connecteur Hello recherche des objets toofind utiles et résoudre les problèmes de données.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Commencez par sélectionner une **portée**. Vous pouvez rechercher sur la base de données (RDN, le nom de domaine, d’ancrage, sous-arborescence), ou l’état de l’objet hello (toutes les autres options).  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Par exemple, si vous effectuez une recherche dans la sous-arborescence, vous obtenez tous les objets d’une unité d’organisation.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
À partir de cette grille, vous pouvez sélectionner un objet, sélectionnez **propriétés**, et [suivent](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) d’espace de connecteur source hello, via le métaverse hello et l’espace de connecteur toohello cible.

### <a name="changing-hello-ad-ds-account-password"></a>Modification de mot de passe de compte hello AD DS
Si vous modifiez le mot de passe de compte hello, hello Service de synchronisation ne pourra plus être en mesure de tooimport/exportation modifications tooon local AD.   Vous pouvez voir les éléments suivants de hello :

- étape d’importation/exportation Hello pour hello Connecteur AD échoue avec l’erreur de « non-start-informations d’identification ».
- Dans l’Observateur d’événements Windows, journal des événements application hello contient une erreur avec l’événement ID 6000 et le message « hello toorun de l’agent « contoso.com » et échoué de la gestion, car les informations d’identification hello n’étaient pas valides. »

tooresolve hello émettre, compte d’utilisateur mise à jour hello AD DS utilisation hello qui suit :


1. Démarrez hello Synchronization Service Manager (Service de synchronisation de début →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Accédez toohello **connecteurs** onglet.
3. Sélectionnez hello le connecteur Active Directory qui est configuré toouse hello compte AD DS.
4. Sous Actions, sélectionnez **Propriétés**.
5. Dans la boîte de dialogue contextuelle hello, sélectionnez se connecter tooActive Directory forêt :
6. nom de la forêt Hello indique hello correspondant locale Active Directory.
7. nom d’utilisateur Hello indique le compte de service d’annuaire hello AD utilisé pour la synchronisation.
8. Entrez hello nouveau mot de passe du compte de hello AD DS dans la zone de texte de mot de passe hello ![Azure AD connecter synchronisation chiffrement clé utilitaire](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Cliquez sur OK toosave hello nouveau mot de passe et redémarrez hello Service de synchronisation tooremove hello ancien mot de passe à partir de la mémoire cache.



## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
