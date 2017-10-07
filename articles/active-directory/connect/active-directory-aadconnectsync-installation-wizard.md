---
title: "Assistant Installation de nouveau en cours d’exécution hello Azure AD Connect | Documents Microsoft"
description: "Explique comment l’Assistant installation hello fonctionne hello deuxième fois que vous exécutez."
keywords: "Assistant d’installation Bonjour Azure AD Connect vous permet de configurer des deuxième fois que vous exécutez hello de paramètres de maintenance"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Synchronisation Azure AD Connect : l’Assistant installation hello en cours d’exécution une deuxième fois.
Hello première fois vous exécutez l’Assistant d’installation Bonjour Azure AD Connect, il vous guide tooconfigure votre installation. Si vous exécutez à nouveau l’Assistant installation Bonjour, il offre des options pour la maintenance.

Vous pouvez trouver l’Assistant installation hello dans le menu Démarrer de hello nommé **Azure AD Connect**.

![Menu Démarrer](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Lorsque vous démarrez l’Assistant installation hello, vous voyez une page avec ces options :

![Page avec une liste de tâches supplémentaires](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Si vous avez installé AD FS avec Azure AD Connect, vous avez davantage d’options. Hello options supplémentaires que vous avez pour ADFS sont documentées dans [gestion ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Sélectionnez une des tâches de hello et cliquez sur **suivant** toocontinue.

> [!IMPORTANT]
> Alors que l’Assistant installation hello est ouvert, toutes les opérations de moteur de synchronisation hello sont suspendues. Assurez-vous que vous fermez l’Assistant installation hello dès que vous avez terminé vos modifications de configuration.
>
>

## <a name="view-current-configuration"></a>Afficher la configuration actuelle
Cette option vous donne un aperçu rapide de vos options actuellement configurées.

![Page avec la liste de toutes les options et leur état](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Cliquez sur **précédent** toogo précédent. Si vous sélectionnez **Exit**, vous fermez l’Assistant installation hello.

## <a name="customize-synchronization-options"></a>Personnaliser les options de synchronisation
Cette option est la configuration de la synchronisation modifications toohello toomake utilisé. Vous consultez un sous-ensemble des options à partir du chemin d’installation de configuration personnalisée hello. Et ce, même si vous avez initialement utilisé l’installation rapide.

* [Ajouter d’autres annuaires](active-directory-aadconnect-get-started-custom.md#connect-your-directories). Pour supprimer un annuaire, consultez [Supprimer un connecteur](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Modifier le filtrage par domaine ou unité d’organisation](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).
* Supprimer le filtrage de groupe.
* [Modifier les fonctionnalités facultatives](active-directory-aadconnect-get-started-custom.md#optional-features).

Bonjour autres options de l’installation initiale de hello ne peut pas être modifiées et ne sont pas disponibles. Ces options sont :

* Modifiez toouse d’attribut hello pour userPrincipalName et sourceAnchor.
* Modifier hello jointure de méthode pour les objets à partir de l’autre forêt.
* Activer le filtrage de groupe.

## <a name="refresh-directory-schema"></a>Actualiser le schéma d’annuaire
Cette option est utilisée si vous avez modifié le schéma de hello dans un de vos locaux sur les forêts AD DS. Par exemple, vous avez peut-être installé Exchange ou mis à niveau le schéma tooa Windows Server 2012 avec les objets périphériques. Dans ce cas, vous avez besoin tooinstruct Azure AD Connect tooread hello schéma à partir des services AD DS et mettre à jour son cache. Cette opération régénère également les règles de synchronisation hello. Si vous ajoutez un schéma d’Exchange hello, par exemple, les règles de synchronisation hello pour Exchange sont ajoutés toohello configuration.

Lorsque vous sélectionnez cette option, tous les répertoires hello dans votre configuration sont répertoriés. Vous pouvez conserver le paramètre par défaut de hello et actualiser toutes les forêts ou désélectionnez certaines d'entre elles.

![Page avec une liste de tous les répertoires dans un environnement de hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Configurer le mode de préproduction
Cette option vous permet de tooenable et désactiver le mode de mise en lots sur le serveur de hello. Vous trouverez plus d’informations sur le mode de préproduction et son utilisation dans [Opérations](active-directory-aadconnectsync-operations.md#staging-mode).

option de Hello indique si la mise en lots est actuellement activé ou désactivé :  
![Option qui s’affiche également état actuel de hello du mode de mise en lots](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange hello état, sélectionnez cette option et la case à cocher Sélectionner ou désélectionner hello.  
![Option qui s’affiche également état actuel de hello du mode de mise en lots](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Modifier la connexion de l’utilisateur
Cette option vous permet de toochange de toofederation de synchronisation de mot de passe ou hello inverse. Vous ne pouvez pas modifier trop**ne configurez pas**.

Pour plus d’informations sur cette option, consultez [connexion de l’utilisateur](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le modèle de configuration hello utilisé par la synchronisation Azure AD Connect dans [approvisionnement déclaratif compréhension](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
