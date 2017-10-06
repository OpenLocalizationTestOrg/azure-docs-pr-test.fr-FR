---
title: "Azure Active Directory Domain Services : Mettre à jour les paramètres DNS pour le réseau virtuel Azure de hello | Documents Microsoft"
description: Prise en main des services de domaine Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Activer Azure Active Directory Domain Services (préversion)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Tâche 4 : mettre à jour les paramètres DNS pour hello réseau virtuel Azure
Bonjour précédant les tâches de configuration, vous avez correctement activé Azure Active Directory Domain Services pour votre annuaire. la tâche suivante Hello est tooensure que les ordinateurs d’un réseau virtuel de hello peuvent se connecter et utilisation de ces services. Dans cet article, vous mettre à jour les paramètres du serveur DNS hello pour votre réseau virtuel toopoint toohello deux adresses IP où Azure des Services de domaine Active Directory est disponible sur le réseau virtuel de hello.

paramètre de serveur DNS tooupdate hello pour le réseau virtuel de hello dans lequel vous avez activé Azure Active Directory Domain Services hello complète comme suit :

1. Hello **vue d’ensemble** onglet répertorie un ensemble de **requis des étapes de configuration** toobe effectuée une fois votre domaine géré est entièrement configuré. première étape de configuration Hello est **paramètres du serveur DNS de mise à jour pour votre réseau virtuel**.

    ![Domain Services - Onglet Vue d’ensemble une fois la configuration terminée](./media/getting-started/domain-services-provisioned-overview.png)

2. Lorsque votre domaine est entièrement configuré, deux adresses IP s’affichent dans cette vignette. Chacune de ces adresses IP représente un contrôleur de domaine pour votre domaine managé.

3. toocopy hello première adresse IP tooclipboard d’adresses, cliquez sur tooit de hello copie bouton suivant. Puis cliquez sur hello **serveurs de configurer le serveur DNS** bouton.

4. Coller la première adresse IP de hello en hello **serveur DNS d’ajouter** textbox Bonjour **serveurs DNS** panneau. Faire défiler horizontalement toohello gauche toocopy hello deuxième adresse IP et le coller dans hello **serveur DNS d’ajouter** zone de texte.

    ![Domain Services - Mettre à jour le DNS](./media/getting-started/domain-services-update-dns.png)

5. Cliquez sur **enregistrer** lorsque vous avez terminé les serveurs DNS tooupdate hello pour le réseau virtuel de hello.

> [!NOTE]
> Machines virtuelles dans un réseau de hello obtenir uniquement les nouveaux paramètres DNS de hello après un redémarrage. Si vous devez les paramètres de DNS tooget hello mis à jour immédiatement, déclencher le redémarrage d’un portail de hello, PowerShell ou hello CLI.
>
>

## <a name="next-step"></a>Étape suivante
[Tâche 5 : activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory](active-directory-ds-getting-started-password-sync.md)
