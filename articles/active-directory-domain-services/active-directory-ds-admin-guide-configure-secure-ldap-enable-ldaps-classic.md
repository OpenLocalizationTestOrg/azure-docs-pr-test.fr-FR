---
title: "aaaConfigure sécurisé LDAP (LDAPS) dans les Services de domaine Active Directory de Azure | Documents Microsoft"
description: "Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine géré par les services de domaine Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
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


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Tâche 3 : activer LDAP sécurisé pour hello de domaine gérés à l’aide du portail Azure classic de hello
tooenable LDAP sécurisé, effectuer hello configuration comme suit :

1. Accédez toohello  **[portail Azure classic](https://manage.windowsazure.com)**.
2. Sélectionnez hello **Active Directory** nœud dans le volet gauche de hello.
3. Sélectionnez le répertoire de hello Azure AD (également désignée tooas « client »), pour lequel vous avez activé les Services de domaine Active Directory de Azure.

    ![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Cliquez sur hello **configurer** onglet.

    ![Configurer l’onglet de l’annuaire](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Faites défiler vers le bas la section toohello intitulée **services de domaine**. Vous devez voir une option intitulée **LDAP sécurisé (LDAPS)** comme indiqué dans hello suivant capture d’écran :

    ![Section de configuration des services de domaine](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Cliquez sur hello **configurer un certificat...**  toobring bouton haut hello **configurer le certificat pour LDAP sécurisé** boîte de dialogue.

    ![Configurer le certificat pour LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Cliquez sur les éléments suivants icône de dossier hello **PFX fichier avec certificat** fichier PFX toospecify hello, qui contient le certificat hello vous souhaitez toouse pour toohello d’accès LDAP sécurisé géré de domaine. Également entrer le mot de passe hello spécifié lors de l’exportation du fichier de certificat toohello PFX hello. Ensuite, cliquez sur hello fait le bouton bas de hello.

    ![Spécifier le mot de passe et le fichier PFX pour LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Hello **services de domaine** section Hello **configurer** onglet doit obtenir grisée et est Bonjour **en attente...**  état pendant quelques minutes. Pendant cette période, le certificat LDAPS hello est vérifié à l’exactitude et LDAP sécurisé est configuré pour votre domaine géré.

    ![LDAP sécurisé - État En attente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Il prend environ 10 minutes too15 tooenable LDAP sécurisé pour votre domaine géré. Si hello fourni de certificat LDAP sécurisé ne correspond pas à hello requis critères, LDAP sécurisé n’est pas activée pour votre annuaire et vous voyez une erreur. Par exemple, nom de domaine hello est incorrect, le certificat de hello a déjà expiré ou va bientôt expire.
   >
   >

9. Lorsque le LDAP sécurisé est activé pour votre domaine géré, hello **en attente...**  message disparaisse. Vous devez voir l’empreinte numérique hello de certificat hello affiché.

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Tâche 4 - activer l’accès LDAP sécurisé sur hello internet
**Tâches facultatives** : Si vous n’envisagez pas de domaine géré de tooaccess hello à l’aide du protocole LDAPS plus hello internet, ignorez cette étape de configuration.

Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Vous devez voir une option trop**hello Activer SECURE LDAP accès via INTERNET** Bonjour **services de domaine** section Hello **configurer** page. Cette option est définie trop**non** par défaut, car internet access toohello gérée domaine via LDAP sécurisé est désactivée par défaut.

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Activer/désactiver **hello Activer SECURE LDAP accès via INTERNET** trop**Oui**. Cliquez sur hello **enregistrer** bouton sur le panneau inférieur hello.
    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Hello **services de domaine** section Hello **configurer** onglet doit obtenir grisée et est Bonjour **en attente...**  état pendant quelques minutes. Après un certain temps, domaine géré tooyour accès internet via LDAP sécurisé est activé.

    ![LDAP sécurisé - État En attente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Il prend environ 10 minutes tooenable accès à internet via LDAP sécurisé à votre domaine géré.
   >
   >
4. Lorsque vous tooyour d’accès LDAP sécurisé gérés domaine via hello internet est activée avec succès, hello **en attente...**  message disparaisse. Vous devez voir des adresses IP externes de hello adresse qui peut être utilisé tooaccess votre annuaire sur LDAPS dans le champ de hello **adresse IP externe pour LDAPS accès**.

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Tâche 5 - configurer DNS tooaccess hello domaine géré à partir de hello internet
**Tâches facultatives** : Si vous n’envisagez pas de domaine géré de tooaccess hello à l’aide du protocole LDAPS plus hello internet, ignorez cette étape de configuration.

Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 4](#task-4---enable-secure-ldap-access-over-the-internet).

Une fois que vous avez activé l’accès LDAP sécurisé sur internet de hello pour votre domaine géré, vous devez tooupdate DNS afin que les ordinateurs clients peuvent trouver ce domaine géré. Extrémité hello de tâche 4, une adresse IP externe est affichée sur hello **configurer** onglet **adresse IP externe pour LDAPS accès**.

Configurez votre fournisseur DNS externe afin que ce nom DNS de hello Hello géré l’adresse IP externe de domaine (par exemple, ' ldaps.contoso100.com') toothis de points. Dans notre exemple, nous devons hello toocreate suivant l’entrée DNS :

    ldaps.contoso100.com  -> 52.165.38.113

C’est tout : vous êtes maintenant toohello tooconnect prêt géré domaine à l’aide de LDAP sécurisé sur hello internet.

> [!WARNING]
> Souvenez-vous que les ordinateurs clients doivent approuver l’émetteur de hello de hello LDAPS certificat toobe en mesure de tooconnect de correctement toohello gérés à l’aide du protocole LDAPS de domaine. Si vous utilisez une autorité de certification d’entreprise ou d’une autorité de certification approuvée publiquement, il est inutile toodo quoi que ce soit dans la mesure où les ordinateurs clients approuver ces émetteurs de certificats. Si vous utilisez un certificat auto-signé, vous devez tooinstall hello publique partie hello un certificat auto-signé dans le magasin de certificats approuvés hello sur l’ordinateur client de hello.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Verrouillage LDAPS accéder au domaine géré de tooyour sur hello internet
> [!NOTE]
> **Tâches facultatives** : Si vous n’avez pas activé LDAPS domaine géré de toohello accès plus hello internet, ignorez cette étape de configuration.
>
>

Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 4](#task-4---enable-secure-ldap-access-over-the-internet).

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
