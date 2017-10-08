---
title: "Azure Active Directory Domain Services : activation | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Tâche 3 : Activer Azure Active Directory Domain Services
Dans cette tâche, vous activez les Services de domaine d’Active Directory Azure (Azure AD DS) pour votre annuaire en procédant comme hello comme suit :

1. Accédez toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le volet gauche de hello, sélectionnez hello **Active Directory** bouton.
3. Sélectionnez le locataire d’Azure Active Directory (Azure AD) hello (répertoire) pour lequel vous souhaitez tooenable Azure AD DS.

    ![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Sur hello **active de la version préliminaire** , cliquez sur hello **configurer** onglet.

    ![Configurer l’onglet de l’annuaire](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Sous **services de domaine**, modifiez hello **activer les services de domaine pour ce répertoire** option trop**Oui**.  
    Les options de configuration Azure des Services de domaine Active Directory supplémentaires s’affichent sur la page de hello.

    ![Activer les services de domaine](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Lorsque vous activez Azure Active Directory Domain Services pour votre client, Azure AD génère et stocke hello Kerberos et NTLM d’informations d’identification hachages qui sont requis pour l’authentification des utilisateurs.
   >
   >
6. Spécifiez hello **le nom de domaine DNS des services de domaine**.

   * nom de domaine par défaut Hello du répertoire de hello (avec un **. onmicrosoft.com** suffixe) est sélectionnée par défaut.

   * Hello liste contient tous les domaines qui ont été configurés pour votre annuaire Azure AD, y compris les deux vérifiés et non vérifiées, les domaines que vous configurez sur hello **domaines** onglet.

   * Vous pouvez également saisir un nom de domaine personnalisé. Dans cet exemple, le nom de domaine personnalisé hello est *contoso100.com*.

     > [!WARNING]
     > préfixe Hello de votre nom de domaine spécifié (par exemple, *contoso100* Bonjour *contoso100.com* nom de domaine) doit contenir au maximum 15 caractères. Vous ne pouvez pas créer un domaine Azure AD DS dont le préfixe contient plus de 15 caractères.
     >
     >
7. Vérifiez que nom de domaine DNS hello choisie pour hello géré domaine n’existe pas déjà dans le réseau virtuel de hello. Plus précisément, vérifiez toosee si :

   * Vous disposez déjà d’un domaine avec hello même nom de domaine DNS sur le réseau virtuel de hello.

   * Hello réseau virtuel que vous avez sélectionné possède une connexion VPN à votre réseau local, et que vous avez un domaine avec hello même nom de domaine DNS de votre réseau local.

   * Vous avez un service cloud existant portant le même nom sur le réseau virtuel de hello.
8. Sélectionnez un réseau virtuel sur lequel vous souhaitez toobe Azure Active Directory Domain Services disponible. Sélectionnez le réseau virtuel de hello et sous-réseau dédié, vous avez créé dans hello **toothis des réseaux virtuels des services de domaine de se connecter** liste déroulante. Également envisager les suivant hello :

   * Assurez-vous que ce réseau virtuel hello que vous avez spécifié appartient tooan région Azure qui est pris en charge par les Services de domaine Active Directory de Azure. tooascertain hello régions Azure où Azure des Services de domaine Active Directory est disponible, consultez [des services Azure par région](https://azure.microsoft.com/regions/#services/).

   * Les réseaux virtuels qui appartiennent région tooa où Azure des Services de domaine Active Directory n’est pas prise en charge ne s’affichent pas dans la liste déroulante de hello.

   * Utilisez un sous-réseau dédié au sein du réseau virtuel de hello pour Azure Active Directory Domain Services. Faire *pas* sélectionnez hello sous-réseau de passerelle. Consultez [Mise en réseau - Éléments à prendre en compte](active-directory-ds-networking.md).

   * De même, les réseaux virtuels qui ont été créés à l’aide du Gestionnaire de ressources Azure n’apparaissent pas dans la liste déroulante de hello. Les réseaux virtuels basés sur Resource Manager ne sont pas pris en charge par Azure AD DS pour le moment.
9. tooenable Services de domaine Active Directory Azure, dans le volet de tâches hello bas hello de page de hello, cliquez sur **enregistrer**.
    * Alors que les Services de domaine Active Directory de Azure est activé pour votre annuaire, page de hello affiche l’état *en attente*.

        ![Fenêtre Activer les services de domaine](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Azure AD DS offre une haute disponibilité pour votre domaine managé. Après avoir activé Azure des Services de domaine Active Directory, les adresses IP hello au domaine dans lequel les services sont disponibles sur le réseau virtuel de hello sont affichent l’un à la fois. adresse IP de la deuxième Hello s’affiche tout d’abord, peu de temps après hello comme bientôt service de hello permet une haute disponibilité pour votre domaine. Lorsque la haute disponibilité est configurée et actif pour votre domaine, vous devez voir deux adresses IP Bonjour **services de domaine** section Hello **configurer** onglet.
        >
        >
    * Après environ 20 minutes too30, première adresse IP hello, au domaine dans lequel les services sont disponibles sur votre réseau virtuel Bonjour **adresse IP** champ hello **configurer** page.

        ![Fenêtre Azure AD DS affichant la première adresse IP configurée](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Lors de la haute disponibilité est opérationnelle pour votre domaine, les deux adresses IP sont affichées sur la page de hello. Votre domaine géré est disponible sur votre réseau virtuel sélectionné à ces deux adresses IP.

10. Notez les deux adresses IP de hello afin que vous pouvez mettre à jour les paramètres DNS hello pour votre réseau virtuel. Ainsi, les ordinateurs virtuels sur le domaine de toohello tooconnect hello réseau virtuel pour les opérations telles que la jonction de domaine.

    ![Fenêtre Azure AD DS affichant les deux adresses IP configurées](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> Selon la taille de hello de votre client Azure AD (par exemple, le nombre d’hello des utilisateurs ou groupes), domaine de synchronisation tooyour géré prend un certain temps. Ce processus de synchronisation se produit en arrière-plan de hello. Pour les clients avec des dizaines de milliers d’objets volumineux, il peut prendre une ou deux jours pour tous les utilisateurs, les appartenances aux groupes et les toobe des informations d’identification synchronisé.
>
>

## <a name="next-step"></a>Étape suivante
[Tâche 4 : mettre à jour les paramètres DNS hello hello réseau virtuel Azure](active-directory-ds-getting-started-update-dns.md)
