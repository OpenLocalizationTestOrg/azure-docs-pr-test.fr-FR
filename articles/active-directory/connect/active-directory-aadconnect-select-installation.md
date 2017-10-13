---
title: "Azure AD Connect : Sélectionner le type d’installation | Microsoft Docs"
description: "Cette rubrique vous montre comment sélectionner le type d’installation à utiliser pour Azure AD Connect"
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
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a>Sélectionner le type d’installation à utiliser pour Azure AD Connect
Azure AD Connect a deux types d’installation pour une nouvelle installation : Express et personnalisée. Cette rubrique vous aide à choisir l’option à utiliser lors de l’installation.

## <a name="express"></a>Express
Express est l’option la plus courante et est utilisée dans environ 90 % des nouvelles installations. Elle a été conçue pour fournir une configuration qui fonctionne dans la plupart des scénarios des clients.

Elle suppose que :

- Vous avez une seule forêt Active Directory locale.
- Vous avez un compte administrateur d’entreprise que vous pouvez utiliser pour l’installation.
- Vous avez moins de 100 000 objets dans votre annuaire Active Directory local.

Vous obtenez :

- La [synchronisation du mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) du système local vers Azure AD pour l’authentification unique.
- Une configuration qui synchronise [les utilisateurs, les groupes, les contacts et les ordinateurs Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).
- La synchronisation de tous les objets éligibles dans tous les domaines et toutes les unités d’organisation.
- La [mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) est activée pour garantir que vous utilisez toujours la dernière version disponible.

Cas où vous pouvez toujours utiliser Express :

- Si vous ne voulez pas synchroniser toutes les unités d’organisation, vous pouvez néanmoins utiliser Express et, dans la dernière page, désélectionner **Démarrer le processus de synchronisation...***. Réexécutez ensuite l’Assistant Installation, changez les unités d’organisation dans les [options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) et activez la synchronisation planifiée.
- Vous voulez activer une des fonctionnalités dans Azure AD Premium, comme la réécriture du mot de passe. Choisissez d’abord Express pour effectuer l’installation initiale. Réexécutez ensuite l’Assistant Installation et changez les [options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Personnalisée
L’installation personnalisée offre beaucoup plus d’options que l’installation Express. Elle doit être utilisée dans tous les cas où la configuration décrite dans la section précédente pour Express n’est pas représentative de votre organisation.

Utilisez-la quand :

- Vous n’avez pas accès à un compte administrateur d’entreprise dans Active Directory.
- Vous avez plusieurs forêts ou vous prévoyez de synchroniser plusieurs forêts à l’avenir.
- Vous avez des domaines dans votre forêt qui ne sont pas accessibles à partir du serveur Connect.
- Vous prévoyez d’utiliser la fédération ou l’authentification directe pour la connexion des utilisateurs.
- Vous avez plus de 100 000 objets et vous devez utiliser un serveur SQL Server complet.
- Vous prévoyez d’utiliser le filtrage par groupe, et pas seulement le filtrage par domaine ou par unité d’organisation.

## <a name="upgrade-from-dirsync"></a>Effectuer une mise à niveau à partir de DirSync
Si vous utilisez actuellement DirSync, suivez les étapes de [Mise à niveau à partir de DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) pour mettre à niveau votre configuration existante. Il existe deux scénarios différents de mise à niveau :

- Mise à niveau sur place pour installer Connect sur le même serveur.
- Déploiement en parallèle pour installer Connect sur un nouveau serveur, alors que le serveur DirSync existant est toujours opérationnel.

## <a name="upgrade-from-azure-ad-sync"></a>Mise à niveau à partir d’Azure AD Sync
Si vous utilisez actuellement Azure AD Sync, vous pouvez suivre les [mêmes étapes](active-directory-aadconnect-upgrade-previous-version.md) que celle de la mise à niveau d’une version de Connect vers une version plus récente. Il existe deux scénarios différents de mise à niveau :

- Mise à niveau sur place pour installer Connect sur le même serveur.
- Migration via une instance distincte pour installer Connect sur un nouveau serveur, alors que le serveur Azure AD Sync existant est toujours opérationnel.

## <a name="migrate-from-fim2010-or-mim2016"></a>Migrer depuis FIM2010 ou MIM2016
Si vous utilisez actuellement Forefront Identity Manager 2010 ou Microsoft Identity Manager 2016 avec le connecteur Azure AD, votre seule option est une migration. Suivez les étapes décrites dans [Migration via une instance distincte](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). Dans les étapes, remplacez les mentions d’Azure AD Sync par FIM2010/MIM2016.

## <a name="next-steps"></a>Étapes suivantes
Selon l’option que vous avez choisie, utilisez la table des matières à gauche pour trouver votre article avec les étapes détaillées.
