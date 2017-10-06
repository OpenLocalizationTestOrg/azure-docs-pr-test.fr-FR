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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Mettre à jour les paramètres DNS pour hello réseau virtuel Azure
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Tâche 4 : Mettre à jour les paramètres DNS pour hello réseau virtuel Azure
Bonjour précédant les tâches de configuration, vous avez correctement activé Azure Active Directory Domain Services pour votre annuaire. la tâche suivante Hello est tooensure que les ordinateurs d’un réseau virtuel de hello peuvent se connecter et utilisation de ces services. Dans cet article, vous mettre à jour les paramètres du serveur DNS hello pour votre réseau virtuel toopoint toohello deux adresses IP où Azure des Services de domaine Active Directory est disponible sur le réseau virtuel de hello.

> [!NOTE]
> Une fois que vous avez activé Azure Active Directory Domain Services pour le répertoire de hello, notez les adresses IP hello pour Azure Active Directory Domain Services qui s’affichent sur hello **configurer** onglet de votre annuaire.
>
>

paramètre de serveur DNS tooupdate hello pour le réseau virtuel de hello dans lequel vous avez activé Azure Active Directory Domain Services hello complète comme suit :

1. Accédez toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le volet gauche de hello, sélectionnez **réseaux**.  
    Hello **réseaux** fenêtre s’ouvre.

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. Sur hello **réseaux virtuels** onglet, le réseau virtuel de select hello dans lequel vous avez activé Azure des Services de domaine Active Directory tooview ses propriétés.
4. Cliquez sur hello **configurer** onglet.

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. Bonjour **serveurs DNS** section, entrez les deux adresses IP hello qui étaient affichés dans hello **Services de domaine** section hello **configurer** onglet de votre annuaire.
6. Cliquez sur les paramètres du serveur DNS toosave hello pour ce réseau virtuel, dans le volet de tâches hello bas hello de fenêtre hello, **enregistrer**.

   ![Mettre à jour les paramètres du serveur DNS hello pour le réseau virtuel de hello](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Machines virtuelles dans un réseau de hello obtenir uniquement les nouveaux paramètres DNS de hello après un redémarrage. Si vous devez les paramètres de DNS tooget hello mis à jour immédiatement, déclencher le redémarrage d’un portail de hello, PowerShell ou hello CLI.
>
>

## <a name="next-steps"></a>Étapes suivantes
Tâche 5 : [activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory](active-directory-ds-getting-started-password-sync.md)
