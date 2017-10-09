---
title: "aaaConfigure sécurisé LDAP (LDAPS) dans les Services de domaine Active Directory de Azure | Documents Microsoft"
description: "Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine géré par les services de domaine Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services

## <a name="before-you-begin"></a>Avant de commencer
Vérifiez que vous avez effectué [tâche 2 - tooa de certificat LDAP sécurisé exportation hello. Le fichier PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Choisir toouse hello aperçu expérience du portail Azure ou hello toocomplete de portail classique Azure cette tâche.
> [!div class="op_single_selector"]
> * **Portail Azure (aperçu)**: [Enable secure LDAP à l’aide de hello portail Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Portail Azure classic**: [Enable secure LDAP à l’aide du portail Azure classic de hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Tâche 3 : activer LDAP sécurisé pour hello de domaine gérés à l’aide de hello portail Azure (aperçu)
tooenable LDAP sécurisé, effectuer hello configuration comme suit :

1. Accédez toohello  **[portail Azure](https://portal.azure.com)**.

2. Rechercher des services de domaine Bonjour **recherche les ressources** zone de recherche. Sélectionnez **les Services de domaine Active Directory de Azure** à partir du résultat de recherche hello. Hello **les Services de domaine Active Directory de Azure** panneau répertorie votre domaine géré.

    ![Rechercher le domaine managé en cours d’approvisionnement](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Cliquez sur nom hello hello géré (par exemple, « contoso100.com ») de domaine toosee plus de détails sur le domaine de hello.

    ![Domain Services - État d’approvisionnement](./media/getting-started/domain-services-provisioning-state.png)

3. Cliquez sur **LDAP sécurisé** hello volet de navigation.

    ![Domain Services - Panneau LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Par défaut, accès tooyour managé domaine LDAP sécurisé est désactivé. Activer/désactiver **LDAP sécurisé** trop**activer**.

    ![Activer LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. Par défaut, tooyour d’accès LDAP sécurisé gérés domaine via hello qu'internet est désactivée. Activer/désactiver **autoriser l’accès LDAP sécurisé sur hello internet** trop**activer**, si vous le souhaitez. 

6. Cliquez sur suivant d’icône hello dossier **. Fichier PFX avec certificat LDAP sécurisé**. Spécifier le fichier PFX de hello chemin d’accès toohello avec certificat hello pour accès toohello managé domaine LDAP sécurisé.

7. Spécifiez hello **toodecrypt de mot de passe. Le fichier PFX**. Fournir hello même mot de passe utilisé lors de l’exportation du fichier de certificat toohello PFX hello.

8. Lorsque vous avez terminé, cliquez sur hello **enregistrer** bouton.

9. Vous voyez une notification qui vous informe de que LDAP sécurisé est configuré pour le domaine géré de hello. Jusqu'à ce que cette opération est terminée, vous ne pouvez pas modifier d’autres paramètres pour le domaine de hello.

    ![Configuration de LDAP sécurisé pour le domaine géré de hello](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Il prend environ 10 minutes too15 tooenable LDAP sécurisé pour votre domaine géré. Si hello fourni de certificat LDAP sécurisé ne correspond pas à hello requis critères, LDAP sécurisé n’est pas activée pour votre annuaire et vous voyez une erreur. Par exemple, nom de domaine hello est incorrect, le certificat de hello a déjà expiré ou va bientôt expire. Dans ce cas, réessayez avec un certificat valide.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Tâche 4 - configurer DNS tooaccess hello domaine géré à partir de hello internet
> [!NOTE]
> **Tâches facultatives** : Si vous n’envisagez pas de domaine géré de tooaccess hello à l’aide du protocole LDAPS plus hello internet, ignorez cette étape de configuration.
>
>

Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Une fois que vous avez activé l’accès LDAP sécurisé sur internet de hello pour votre domaine géré, vous devez tooupdate DNS afin que les ordinateurs clients peuvent trouver ce domaine géré. Extrémité hello de tâche 3, une adresse IP externe est affichée sur hello **propriétés** lame **adresse IP externe pour LDAPS accès**.

Configurez votre fournisseur DNS externe afin que ce nom DNS de hello Hello géré l’adresse IP externe de domaine (par exemple, ' ldaps.contoso100.com') toothis de points. Dans notre exemple, nous devons hello toocreate suivant l’entrée DNS :

    ldaps.contoso100.com  -> 52.165.38.113

C’est tout : vous êtes maintenant toohello tooconnect prêt géré domaine à l’aide de LDAP sécurisé sur hello internet.

> [!WARNING]
> Souvenez-vous que les ordinateurs clients doivent approuver l’émetteur de hello de hello LDAPS certificat toobe en mesure de tooconnect de correctement toohello gérés à l’aide du protocole LDAPS de domaine. Si vous utilisez une autorité de certification approuvée publiquement, il est inutile toodo quoi que ce soit dans la mesure où les ordinateurs clients approuver ces émetteurs de certificats. Si vous utilisez un certificat auto-signé, installez hello publique partie hello un certificat auto-signé dans le magasin de certificats approuvés hello sur l’ordinateur client de hello.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Tâche 5 : verrouillage LDAPS accéder tooyour géré domaine sur hello internet
> [!NOTE]
> **Tâches facultatives** : Si vous n’avez pas activé LDAPS domaine géré de toohello accès plus hello internet, ignorez cette étape de configuration.
>
>

Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Exposition de votre domaine géré pour l’accès LDAPS sur hello internet représente une menace pour la sécurité. Bonjour domaine géré est accessible à partir de hello internet au port hello utilisé pour LDAP sécurisé (autrement dit, le port 636). Par conséquent, vous pouvez choisir toorestrict accès toohello géré domaine toospecific connu des adresses IP. Pour améliorer la sécurité, créez un groupe de sécurité réseau (NSG) et l’associer à sous-réseau hello où vous avez activé les Services de domaine Active Directory de Azure.

Hello tableau suivant illustre un exemple de groupe de sécurité réseau que vous pouvez configurer, toolock vers le bas un accès LDAP sécurisé sur hello internet. Hello NSG contient un ensemble de règles qui autorisent l’accès LDAPS entrant sur le port TCP 636 uniquement à partir d’un ensemble spécifique d’adresses IP. Hello par défaut 'DenyAll' règle s’applique tooall reste du trafic entrant de hello internet. Hello NSG règle tooallow LDAPS d’accès sur hello internet à partir d’adresses IP spécifiées a une priorité supérieure à la règle de DenyAll NSG de hello.

![Exemple NSG toosecure LDAPS d’accès sur hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Plus d’informations** - [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Administrer un domaine géré par les services de domaine Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
* [Gérer la stratégie de groupe sur un domaine géré par les services de domaine Azure AD](active-directory-ds-admin-guide-administer-group-policy.md)
* [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md)
* [Créer des groupes de sécurité réseau à l’aide du portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
