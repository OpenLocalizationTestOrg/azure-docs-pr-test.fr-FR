---
title: "opérations d’Active Directory Connect Health aaaAzure"
description: "Cet article décrit les opérations supplémentaires pouvant être effectuées après le déploiement d’Azure AD Connect Health."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Opérations Azure Active Directory Connect Health
Cette rubrique décrit hello différentes opérations que vous pouvez effectuer à l’aide d’Azure Active Directory (Azure AD) Connect Health.

## <a name="enable-email-notifications"></a>Activer les notifications par courrier électronique
Vous pouvez configurer des notifications par courrier électronique de hello Azure AD Connect Health service toosend lorsque les alertes indiquent que votre infrastructure d’identité n’est pas intègre. Cela se produit quand une alerte est générée et quand elle est résolue.

![Capture d’écran des paramètres de notifications par courrier électronique Azure AD Connect Health](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> Les notifications par courrier électronique sont activées par défaut.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>notifications par courrier électronique tooenable Azure AD Connect Health
1. Ouvrez hello **alertes** panneau pour le service hello pour lequel vous souhaitez la notification par courrier électronique de tooreceive.
2. Dans la barre d’action hello, cliquez sur **paramètres de Notification**.
3. Commutateur de notification par courrier électronique hello, sélectionnez **ON**.
4. Activez la case à cocher hello si vous souhaitez que les notifications par courrier électronique de tous les administrateurs généraux tooreceive.
5. Si vous souhaitez que les notifications par courrier électronique de tooreceive à toutes les autres adresses de messagerie, spécifiez-les dans hello **destinataires de courrier électronique supplémentaires** boîte. tooremove une adresse de messagerie dans cette liste, cliquez sur entrée de hello et sélectionnez **supprimer**.
6. modifications de hello toofinalize, cliquez sur **enregistrer**. Les modifications prennent effet après l’enregistrement.

## <a name="delete-a-server-or-service-instance"></a>Supprimer une instance de serveur ou de service

Dans certains cas, vous pourriez tooremove un serveur en cours d’analyse. Voici ce que vous devez tooknow tooremove un serveur à partir du service de hello Azure AD Connect Health.

Lorsque vous supprimez un serveur, tenez compte des éléments suivants de hello :

* Cette action arrête la collecte des données de ce serveur. Ce serveur est supprimé de hello service d’analyse. Une fois cette action, vous n’êtes pas en mesure de tooview nouvelles alertes, analyse ou données analytique d’utilisation pour ce serveur.
* Cette action ne désinstalle pas hello Agent d’intégrité de votre serveur. Si vous n’avez pas désinstallé hello Agent d’intégrité avant d’effectuer cette étape, vous pouvez voir les erreurs toohello connexes Agent d’intégrité sur le serveur de hello.
* Cette action ne supprime pas les données de hello déjà collectées à partir de ce serveur. Suppression des données conformément aux hello stratégie de rétention de données Azure.
* Après avoir effectué cette action, si vous souhaitez que l’analyse de toostart hello même serveur, vous devez désinstaller et réinstaller l’Agent d’intégrité de hello sur ce serveur.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete un serveur à partir du service de hello Azure AD Connect Health
Azure AD Connect Health pour les services de fédération Active Directory (ADFS) et Azure AD Connect (Synchronisation) :

1. Ouvrez hello **serveur** Panneau de hello **liste de serveurs** panneau en sélectionnant toobe de nom de serveur hello supprimé.
2. Sur hello **Server** panneau, à partir de la barre d’action hello, cliquez sur **supprimer**.
3. Confirmez en tapant le nom du serveur hello dans la boîte de confirmation hello.
4. Cliquez sur **Supprimer**.

Azure AD Connect Health pour Azure Active Directory Domain Services :

1. Ouvrez hello **contrôleurs de domaine** tableau de bord.
2. Sélectionnez hello toobe de contrôleur de domaine supprimé.
3. Dans la barre d’action hello, cliquez sur **supprimer sélectionné**.
4. Confirmer le serveur de hello action toodelete hello.
5. Cliquez sur **Supprimer**.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Supprimer une instance de service du service Azure AD Connect Health
Dans certains cas, vous pourriez tooremove une instance de service. Voici ce que vous devez tooknow tooremove un service de l’instance de service de hello Azure AD Connect Health.

Lorsque vous supprimez une instance de service, tenez compte des éléments suivants de hello :

* Cette action supprime instance actuelle du service hello hello service d’analyse.
* Cette action ne pas désinstaller ou supprimer hello Agent d’intégrité à partir de n’importe quel serveur hello qui ont été analysés dans le cadre de cette instance de service. Si vous n’avez pas désinstallé hello Agent d’intégrité avant d’effectuer cette étape, vous pouvez voir toohello connexes d’erreurs Agent d’intégrité sur les serveurs de hello.
* Toutes les données de cette instance de service est supprimé conformément aux hello stratégie de rétention de données Azure.
* Après avoir effectué cette action, si vous souhaitez toostart hello service de surveillance, désinstaller et réinstaller hello Agent d’intégrité sur tous les serveurs hello. Après avoir effectué cette action, si vous souhaitez toostart analyse hello même serveur, désinstaller, réinstaller et inscrire hello Agent d’intégrité sur ce serveur.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete une instance de service à partir du service de hello Azure AD Connect Health
1. Ouvrez hello **Service** Panneau de hello **Service liste** panneau en sélectionnant l’identificateur de service hello (nom de la batterie) que vous souhaitez tooremove.
2. Sur hello **Server** panneau, à partir de la barre d’action hello, cliquez sur **supprimer**.
3. Confirmez en tapant le nom du service hello dans la boîte de confirmation hello (par exemple : sts.contoso.com).
4. Cliquez sur **Supprimer**.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Gérer l’accès à l’aide du contrôle d’accès en fonction du rôle
[Contrôle d’accès en fonction du rôle (RBAC)](../role-based-access-control-configure.md) pour Azure AD Connect Health fournit l’accès toousers et des groupes autres que les administrateurs généraux. RBAC attribue les rôles toohello destinée utilisateurs et groupes et fournit un mécanisme toolimit les administrateurs généraux hello dans votre annuaire.

### <a name="roles"></a>contrôleur
Azure AD Connect Health prend en charge hello suivant rôles intégrés :

| Rôle | Autorisations |
| --- | --- |
| Propriétaire |Les propriétaires peuvent *gérer l’accès* (par exemple, attribuer un rôle tooa utilisateur ou groupe), *afficher toutes les informations* (par exemple, afficher les alertes) à partir du portail de hello, et *modifier les paramètres* () notifications par courrier électronique, par exemple) dans Azure AD Connect Health. <br>Par défaut, ce rôle est affecté de manière immuable aux administrateurs généraux Azure AD. |
| Collaborateur |Collaborateurs peuvent *afficher toutes les informations* (par exemple, afficher les alertes) à partir du portail de hello, et *modifier les paramètres* (par exemple, notifications par courrier électronique) dans Azure AD Connect Health. |
| Lecteur |Lecteurs peuvent *afficher toutes les informations* (par exemple, afficher les alertes) à partir du portail hello dans Azure AD Connect Health. |

Tous les autres rôles (par exemple, les administrateurs de l’accès utilisateur ou les utilisateurs de DevTest Labs) n’ont aucun tooaccess impact dans Azure AD Connect Health, même si les rôles hello sont disponibles dans l’utilisation du portail hello.

### <a name="access-scope"></a>Étendue de l’accès
Azure AD Connect Health prend en charge la gestion des accès à deux niveaux :

* **Toutes les instances de service**: il s’agit de hello recommandé de chemin d’accès dans la plupart des cas. Il contrôle l’accès pour toutes les instances de service (par exemple, une batterie de serveurs AD FS) parmi tous les types de rôle surveillées par Azure AD Connect Health.
* **Instance de service**: dans certains cas, vous devrez peut-être accès toosegregate basés sur les types de rôle ou à une instance de service. Dans ce cas, vous pouvez gérer l’accès au niveau instance de service hello.  

Si un utilisateur final a accès au répertoire de hello ou service l’autorisation est accordée au niveau de l’instance.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Autoriser les utilisateurs ou groupes d’accès tooAzure AD Connect Health
Hello étapes suivantes montrent comment accéder à tooallow.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Étape 1 : Sélectionnez l’étendue d’accès appropriées hello
tooallow un utilisateur l’accès à hello *toutes les instances de service* niveau au sein d’Azure AD Connect Health, panneau principal de hello ouvert dans Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Étape 2 : Ajouter des utilisateurs et des groupes, et affecter des rôles
1. À partir de hello **configurer** , cliquez sur **utilisateurs**.<br>
   ![Capture d’écran du panneau principal de contrôle d’accès en fonction du rôle d’Azure AD Connect Health, avec Utilisateurs mis en surbrillance](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Sélectionnez **Ajouter**.
3. Bonjour **sélectionner un rôle** volet, sélectionnez un rôle (par exemple, **propriétaire**).<br>
   ![Capture d’écran de la fenêtre Utilisateurs de contrôle d’accès en fonction du rôle d’Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Nom de type hello ou l’identificateur de hello ciblées utilisateur ou un groupe. Vous pouvez sélectionner un ou plusieurs utilisateurs ou groupes au hello même temps. Cliquez sur **Sélectionner**.
   ![Capture d’écran de la fenêtre Utilisateurs de contrôle d’accès en fonction du rôle d’Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Sélectionnez **OK**.<br>
6. Une fois l’attribution de rôle hello terminée, hello utilisateurs et groupes s’affichent dans la liste de hello.<br>
   ![Capture d’écran de la fenêtre Utilisateurs de contrôle d’accès en fonction du rôle d’Azure AD Connect Health, avec les nouveaux utilisateurs mis en surbrillance](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Hello apparaît maintenant aux utilisateurs et groupes ont accès, en fonction de tootheir affecté des rôles.

> [!NOTE]
> * Les administrateurs globaux ont toujours des opérations de hello tooall un accès complet, mais les comptes d’administrateur global ne sont pas présentes dans hello précédant la liste.
> * fonctionnalité d’inviter des utilisateurs Hello n’est pas pris en charge dans Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Étape 3 : Emplacement du panneau partage hello avec des utilisateurs ou des groupes
1. Une fois les autorisations affectées, un utilisateur peut accéder à Azure AD Connect Health à [cette adresse](http://aka.ms/aadconnecthealth).
2. Dans Panneau de hello, utilisateur de hello pouvez épingler les lames hello ou différentes parties du tableau de bord toohello. Cliquez simplement sur hello **toodashboard du code confidentiel** icône.<br>
   ![Capture d’écran du panneau de contrôle d’accès en fonction du rôle d’Azure AD Connect Health, avec l’icône d’épinglage mise en surbrillance](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Un utilisateur avec le rôle de lecteur hello affecté n’est pas extension d’Azure AD Connect Health tooget en mesure de hello Azure Marketplace. utilisateur de Hello Impossible d’effectuer jusqu'à hello nécessaires toodo opération « créer ». Hello utilisateur peut toujours obtenir toohello panneau par toohello va précédant le lien. Pour une utilisation ultérieure, utilisateur de hello pouvez épingler toohello du tableau de bord panneau hello.
>
>

### <a name="remove-users-or-groups"></a>Supprimer des utilisateurs ou des groupes
Vous pouvez supprimer un utilisateur ou un groupe ajouté tooAzure AD RBAC de contrôle d’intégrité se connecter. Cliquez simplement avec le bouton droit à l’utilisateur de hello ou un groupe et sélectionnez **supprimer**.<br>
![Capture d’écran de la fenêtre Utilisateurs de contrôle d’accès en fonction du rôle d’Azure AD Connect Health, avec Supprimer mis en surbrillance](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Étapes suivantes
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installation de l’agent Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilisation d'Azure AD Connect Health pour la synchronisation (en Anglais)](active-directory-aadconnect-health-sync.md)
* [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md)
* [Forum Aux Questions (FAQ) Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historique des versions d’Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
