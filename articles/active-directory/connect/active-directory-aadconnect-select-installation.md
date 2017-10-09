---
title: "Azure AD Connect : Sélectionner le type d’installation | Microsoft Docs"
description: "Cette rubrique vous explique comment comment tooselect hello type d’installation toouse pour Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Sélectionnez le toouse de type d’installation pour Azure AD Connect
Azure AD Connect a deux types d’installation pour une nouvelle installation : Express et personnalisée. Cette rubrique vous aide à toodecide qui option toouse pendant l’installation.

## <a name="express"></a>Express
Express est l’option la plus courante hello et est utilisé par environ 90 % de toutes les nouvelles installations. Il a été conçu tooprovide une configuration qui fonctionne pour les scénarios de client les plus courants hello.

Elle suppose que :

- Vous avez une seule forêt Active Directory locale.
- Vous avez un compte administrateur d’entreprise que vous pouvez utiliser pour l’installation de hello.
- Vous avez moins de 100 000 objets dans votre annuaire Active Directory local.

Vous obtenez :

- [Synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) de tooAzure local AD pour l’authentification unique.
- Une configuration qui synchronise [les utilisateurs, les groupes, les contacts et les ordinateurs Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).
- La synchronisation de tous les objets éligibles dans tous les domaines et toutes les unités d’organisation.
- [Mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) est activé toomake que vous utilisez toujours hello version la plus récente.

Cas où vous pouvez toujours utiliser Express :

- Si vous ne souhaitez pas toosynchronize tous d’unités d’organisation, vous pouvez toujours utiliser Express et sur la dernière page de hello, désélectionnez **démarrer le processus de synchronisation hello...** *. Ensuite, réexécutez l’Assistant installation de hello et modifier les unités d’organisation hello dans [les options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) et activer la synchronisation planifiée.
- Vous souhaitez tooenable l’une des fonctionnalités hello dans Azure AD Premium, telles que l’écriture différée de mot de passe. Effectuez tout d’abord tooget express hello initiale l’installation est terminée. Ensuite, réexécutez l’Assistant installation de hello et modifier hello [les options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Personnalisée
chemin d’accès personnalisé de Hello permet de nombreuses autres options que la version express. Elle doit être utilisée dans tous les cas où la configuration de hello décrite dans la section précédente pour express n’est pas représentative de votre organisation.

Utilisez-la quand :

- Vous n’avez pas de compte d’administrateur accès tooan entreprise dans Active Directory.
- Vous avez plusieurs forêts ou que vous envisagez de toosynchronize plusieurs forêts dans hello futures.
- Vous avez des domaines dans votre forêt n’est pas accessible à partir du serveur de connexion hello.
- Vous envisagez de fédération de toouse ou de l’authentification directe pour la connexion d’utilisateur.
- Vous disposez de plus de 100 000 objets et que vous devez toouse une complète de SQL Server.
- Vous envisagez de toouse basée sur le groupe de filtrage et non seulement le domaine ou le filtrage basé sur une unité d’organisation.

## <a name="upgrade-from-dirsync"></a>Mise à niveau à partir de DirSync
Si vous utilisez actuellement la synchronisation d’annuaire, puis suivez les étapes de hello dans [mise à niveau à partir de la synchronisation d’annuaire](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade votre configuration existante. Il existe deux scénarios différents de mise à niveau :

- Connecter tooinstall de mise à niveau sur place sur hello même serveur.
- Parallèle déploiement tooinstall se connecter sur un nouveau serveur alors que le serveur de synchronisation d’annuaire hello existant est toujours opérationnel.

## <a name="upgrade-from-azure-ad-sync"></a>Mise à niveau à partir d’Azure AD Sync
Si vous utilisez Azure AD Sync, vous pouvez suivre hello [mêmes étapes](active-directory-aadconnect-upgrade-previous-version.md) comme lorsque vous mettez à niveau à partir d’une connexion version tooa plus récente. Il existe deux scénarios différents de mise à niveau :

- Connecter tooinstall de mise à niveau sur place sur hello même serveur.
- Migration de basculement tooinstall se connecter sur un nouveau serveur lors de serveur de synchronisation Azure AD existant hello est toujours opérationnel.

## <a name="migrate-from-fim2010-or-mim2016"></a>Migrer depuis FIM2010 ou MIM2016
Si vous utilisez actuellement Microsoft Forefront Identity Manager 2010 ou Microsoft Identity Manager 2016 avec hello connecteur Azure AD, votre seule option est une migration. Suivez les étapes de hello décrites dans [basculement-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). Dans les étapes de hello, remplacez toute mention d’Azure AD Sync avec FIM 2010/MIM2016.

## <a name="next-steps"></a>Étapes suivantes
En fonction de l’option de hello sélectionnée toouse, utilisez le tableau de hello de toofind gauche du contenu toohello votre article avec hello les étapes détaillées.
