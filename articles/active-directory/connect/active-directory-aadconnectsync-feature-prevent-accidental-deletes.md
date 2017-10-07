---
title: "Azure AD Connect sync : prévention des suppressions accidentelles | Microsoft Docs"
description: "Cette rubrique décrit hello empêcher la fonctionnalité de suppressions accidentelles (ce qui empêche les suppressions accidentelles) dans Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Azure AD Connect Sync : Prévention des suppressions accidentelles
Cette rubrique décrit hello empêcher la fonctionnalité de suppressions accidentelles (ce qui empêche les suppressions accidentelles) dans Azure AD Connect.

Lors de l’installation d’Azure AD Connect, empêche accidentelle suppressions est activée par défaut et configuré toonot autoriser une exportation avec plus de 500 suppressions. Cette fonctionnalité est conçue tooprotect vous à partir de la configuration accidentelle et changé tooyour locale active qui est susceptible d’affecter plusieurs utilisateurs et autres objets.

## <a name="what-is-prevent-accidental-deletes"></a>Présentation de la prévention des suppressions accidentelles
Voici quelques scénarios courants de nombreuses suppressions :

* Change également[filtrage](active-directory-aadconnectsync-configure-filtering.md) où l’intégralité d’un [unité d’organisation](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) ou [domaine](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) n’est pas cochée.
* Tous les objets d’une unité d'organisation sont supprimés.
* Une unité d’organisation est renommée tous les objets qu’elle contient sont considérées comme toobe hors de portée pour la synchronisation.

valeur par défaut Hello 500 objets peut être modifiée avec PowerShell à l’aide de `Enable-ADSyncExportDeletionThreshold`. Vous devez configurer cette taille de hello toofit la valeur de votre organisation. Étant donné que le Planificateur de synchronisation hello s’exécute toutes les 30 minutes, valeur de hello est nombre hello de suppressions vu dans les 30 minutes.

S’il y a trop de suppressions intermédiaires toobe exportées tooAzure AD, puis hello d’exportation s’arrête et que vous recevez un message électronique comme suit :

![E-mail de prévention des suppressions accidentelles](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Bonjour (contact technique). À (heure) hello service de synchronisation d’identité a détecté que nombre hello de suppressions dépassé hello suppression configuré (nom d’organisation). En tout, (nombre) objets ont été envoyés pour suppression au cours de ce cycle de synchronisation des identités. Il atteint ou dépassé le seuil hello configuré la suppression d’objets de (nombre). Nous devons vous confirmation de tooprovide ces suppressions doivent être traité avant que nous sera effectuée. Consultez hello empêche les suppressions accidentelles pour plus d’informations sur l’erreur hello répertoriée dans ce message électronique.*
>
> 

Vous pouvez également afficher le statut de hello `stopped-deletion-threshold-exceeded` lorsque vous consultez Bonjour **Synchronization Service Manager** l’interface utilisateur pour le profil d’exportation hello.
![Interface utilisateur Sync Service Manager de prévention des suppressions accidentelles](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Si l'événement n'était pas prévu, examinez la situation et corrigez-la si nécessaire. toosee sur toobe supprimé, les objets hello suivant :

1. Démarrer **Service de synchronisation** à partir du Menu Démarrer de hello.
2. Accédez trop**connecteurs**.
3. Sélectionnez hello connecteur avec type **Azure Active Directory**.
4. Sous **Actions** toohello à droite, sélectionnez **espace de connecteur de recherche**.
5. Bonjour publicitaires sous **étendue**, sélectionnez **déconnecté depuis** et choisissez une heure Bonjour passées. Cliquez sur **Rechercher**. Cette page fournit une vue de tous les objets sur toobe supprimé. En cliquant sur chaque élément, vous pouvez obtenir des informations supplémentaires sur l’objet de hello. Vous pouvez également cliquer sur **colonne paramètre** tooadd supplémentaire attributs toobe visible dans la grille de hello.

![Espace de connecteur de recherche](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

Si toutes les suppressions de hello sont souhaitées, puis hello suivant :

1. tooretrieve hello suppression seuil actuel, exécutez l’applet de commande PowerShell hello `Get-ADSyncExportDeletionThreshold`. Indiquez un compte et un mot de passe d’administrateur général Azure AD. Hello par défaut est 500.
2. tootemporarily désactiver cette protection et laisser les suppressions parcourez, exécutez l’applet de commande PowerShell hello : `Disable-ADSyncExportDeletionThreshold`. Indiquez un compte et un mot de passe d’administrateur général Azure AD.
   ![Informations d'identification](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Action de hello hello le connecteur Active Directory étant toujours sélectionnée, sélectionnez **exécuter** et sélectionnez **exporter**.
4. toore-activer la protection hello, exécutez l’applet de commande PowerShell hello : `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. Remplacez 500 par valeur hello que vous remarqué lors de la récupération du seuil de suppression actuelle hello. Indiquez un compte et un mot de passe d’administrateur général Azure AD.

## <a name="next-steps"></a>Étapes suivantes
**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
