---
title: 'Azure AD Connect Sync : configurer le filtrage | Microsoft Docs'
description: Explique comment tooconfigure filtrage de synchronisation Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Azure AD Connect Sync : Configurer le filtrage
L’utilisation du filtrage vous permet de contrôler les objets de votre annuaire local qui doivent apparaître dans Azure Active Directory (Azure AD). configuration par défaut de Hello prend tous les objets dans tous les domaines dans des forêts hello configuré. En règle générale, il s’agit de hello configuration recommandée. Les utilisateurs qui utilisent les charges de travail Office 365, telles qu’Exchange Online et Skype Entreprise, peuvent tirer parti d’une liste d’adresses globale complète pour envoyer des courriers électroniques et appeler tout le monde. Configuration par défaut de hello, ils auraient pas hello que même expérience qu’ils auraient pas avec une implémentation locale d’Exchange ou Lync.

Dans certains cas, toutefois, que vous devez effectuer certaines modifications de configuration par défaut toohello. Voici quelques exemples :

* Vous envisagez de toouse hello [topologie de répertoire Active Directory multi-Azure](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant). Vous devez tooapply une toocontrol filtre les objets qui sont synchronisés tooa particulier Azure AD active.
* Vous exécutez un pilote pour Azure ou Office 365 et souhaitez uniquement disposer d’un sous-ensemble d’utilisateurs dans Azure AD. Dans le pilote de petite hello, il n’est pas important toohave une liste d’adresses globale toodemonstrate hello une fonction complète.
* Vous disposez d’un grand nombre de comptes de service et d’autres comptes non personnels dont vous ne voulez pas dans Azure AD.
* Pour des raisons de conformité, vous ne supprimez aucun compte d’utilisateur local. Vous vous contentez de les désactiver. Mais dans Azure AD, vous souhaitez seulement toobe comptes actifs présents.

Cet article décrit comment tooconfigure hello différentes méthodes de filtrage.

> [!IMPORTANT]
> Microsoft ne prend en charge de modification ou d’exploitation de synchronisation Azure AD Connect en dehors des actions de hello sont documentées de façon formelle. Ces actions peuvent entraîner un état de synchronisation Azure AD Connect incohérent ou non pris en charge. Par conséquent, Microsoft ne peut pas fournir de support technique pour ces déploiements.

## <a name="basics-and-important-notes"></a>Principes de base et remarques importantes
Dans Azure AD Connect Sync, vous pouvez activer le filtrage à tout moment. Si vous démarrez avec une configuration par défaut de la synchronisation d’annuaires et configurez le filtrage, hello objets qui sont filtrées ne sont plus synchronisé tooAzure AD. En raison de ce changement, tous les objets présents dans Azure AD précédemment synchronisés puis filtrés sont supprimés d’Azure AD.

Avant de pouvoir apporter des modifications toofiltering, assurez-vous que vous [désactiver la tâche planifiée hello](#disable-scheduled-task) donc vous n’exportez pas accidentellement les modifications que vous n’avez pas encore vérifié toobe correct.

Étant donné que le filtrage peut supprimer plusieurs objets à hello même moment, vous souhaitez toomake assurer que vos nouveaux filtres sont correctes avant de commencer une exportation change tooAzure AD. Une fois que vous avez terminé les étapes de configuration de hello, nous recommandons que vous suivez hello [étapes de vérification](#apply-and-verify-changes) avant d’exporter et d’apporter des modifications tooAzure AD.

tooprotect vous de supprimer plusieurs objets par inadvertance, hello fonctionnalité «[empêcher des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)» est activé par défaut. Si vous supprimez plusieurs objets en raison toofiltering (500 par défaut), vous devez les étapes de hello toofollow cette Bonjour tooallow de l’article supprime toogo via tooAzure AD.

Si vous utilisez une build avant novembre 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)), effectuer une modification de configuration de filtre tooa et utiliser la synchronisation de mot de passe, vous devez tootrigger une synchronisation complète de tous les mots de passe après avoir terminé la configuration de hello. Pour savoir comment tootrigger un mot de passe une synchronisation complète, consultez [déclencher une synchronisation complète de tous les mots de passe](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords). Si vous êtes sur la build 1.0.9125 ou à une version ultérieure, puis hello regular **synchronisation complète** action calcule également si les mots de passe doivent être synchronisées et si cette étape supplémentaire n’est plus nécessaire.

Si **utilisateur** objets ont été supprimés par inadvertance dans Azure AD en raison d’une erreur de filtrage, vous pouvez recréer des objets de l’utilisateur hello dans Azure AD en supprimant vos configurations de filtrage. Vous pouvez ensuite resynchroniser vos annuaires. Cette action restaure les utilisateurs de hello à partir de la Corbeille hello dans Azure AD. Toutefois, vous ne pouvez pas annuler la suppression d’autres types d’objets. Par exemple, si vous supprimez accidentellement un groupe de sécurité, et il a été utilisé tooACL une ressource, groupe de hello et son ACL ne peut pas être récupéré.

Azure AD Connect supprime uniquement les objets qu’il a une seule fois considéré toobe dans l’étendue. Si certains objets d’Azure AD ont été créés par un autre moteur de synchronisation et ne figurent pas dans l’étendue, l’ajout d’un filtrage ne les supprime pas. Par exemple, si vous démarrez avec un serveur de synchronisation d’annuaire qui a créé une copie complète de tout le répertoire dans Azure AD, et que vous installez un nouveau serveur de synchronisation Azure AD Connect en parallèle avec le filtrage est activé à partir du début de hello, Azure AD Connect ne supprime pas hello supplémentaire objets qui sont créés par la synchronisation d’annuaire.

configuration de filtrage de Hello est conservée lorsque vous installez ou mettez à niveau de version plus récente de tooa d’Azure AD Connect. Il toujours une meilleure tooverify pratique qui hello configuration n’a pas été modifié par inadvertance après une version plus récente de la mise à niveau tooa avant d’exécuter hello premier cycle de synchronisation.

Si vous avez plusieurs forêts, vous devez appliquer hello filtrage des configurations qui sont décrites dans cette forêt tooevery de rubrique (en supposant que vous souhaitez hello même configuration pour toutes les).

### <a name="disable-hello-scheduled-task"></a>Désactiver la tâche planifiée hello
Planificateur intégré toodisable hello qui déclenche un cycle de synchronisation toutes les 30 minutes, procédez comme suit :

1. Passez l’invite de commandes PowerShell tooa.
2. Exécutez `Set-ADSyncScheduler -SyncCycleEnabled $False` toodisable le planificateur hello.
3. Apportez les modifications hello décrits dans cet article.
4. Exécutez `Set-ADSyncScheduler -SyncCycleEnabled $True` Planificateur de hello tooenable à nouveau.

**Si vous utilisez une version d’Azure AD Connect antérieure à 1.1.105.0**  
tâche planifiée toodisable hello qui déclenche un cycle de synchronisation toutes les trois heures, procédez comme suit :

1. Démarrer **du Planificateur de tâches** de hello **Démarrer** menu.
2. Directement sous **bibliothèque du Planificateur de tâches**, tâche hello de recherche nommé **Azure AD Sync Scheduler**, avec le bouton droit, puis sélectionnez **désactiver**.  
   ![Planificateur de tâche](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. Vous pouvez apporter des modifications de configuration et exécutent le moteur de synchronisation de hello manuellement à partir de hello **Synchronization Service Manager** console.

Une fois que vous avez effectué toutes vos modifications de filtrage, n’oubliez pas toocome précédent et **activer** tâche hello à nouveau.

## <a name="filtering-options"></a>Options de filtrage
Vous pouvez appliquer hello suivant l’outil de synchronisation de répertoire de toohello de types de configuration de filtrage :

* [**Groupe**](#group-based-filtering): filtrage basé sur un groupe unique peut uniquement être configuré sur l’installation initiale à l’aide de l’Assistant installation hello.
* [**Domaine**](#domain-based-filtering): À l’aide de cette option, vous pouvez sélectionner les domaines synchroniser tooAzure AD. Vous pouvez également ajouter et supprimer des domaines de la configuration du moteur de synchronisation hello lorsque vous effectuez une infrastructure de modifications tooyour locale après l’installation de synchronisation Azure AD Connect.
* [**Unité d’organisation (UO) – base**](#organizational-unitbased-filtering): À l’aide de cette option, vous pouvez sélectionner les unités d’organisation synchroniser tooAzure AD. Cette option s’applique à tous les types d’objets présents dans les unités d’organisation sélectionnées.
* [**Basée sur l’attribut**](#attribute-based-filtering): À l’aide de cette option, vous pouvez filtrer les objets en fonction des valeurs d’attribut sur les objets de hello. Vous pouvez également avoir des filtres différents pour différents types d’objets.

Vous pouvez utiliser plusieurs options de filtrage à hello même temps. Par exemple, vous pouvez utiliser le filtrage basé sur une unité d’organisation tooonly inclure des objets dans une unité d’organisation. AT hello même temps, vous pouvez utiliser basée sur les attributs des objets d’hello toofilter filtrage supplémentaire. Lorsque vous utilisez plusieurs méthodes de filtrage, les filtres de hello utilisent une logique « AND » entre les filtres hello.

## <a name="domain-based-filtering"></a>Filtrage basé sur un domaine
Cette section fournit avec hello étapes tooconfigure votre filtre de domaine. Si vous avez ajouté ou supprimé des domaines dans votre forêt après avoir installé Azure AD Connect, vous avez également hello tooupdate configuration de filtrage.

Hello préféré toochange basés sur un domaine de filtrage est en exécutant l’Assistant installation de hello et en modifiant de façon [domaine et le filtrage de l’unité d’organisation](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). l’Assistant installation Hello automatise toutes les tâches de hello sont documentées dans cette rubrique.

Vous devez uniquement suivre ces étapes si vous êtes l’Assistant d’installation ne peut pas toorun hello pour une raison quelconque.

Configuration de filtrage basé sur un domaine se compose des étapes suivantes :

1. [Sélectionnez les domaines hello](#select-domains-to-be-synchronized) que vous souhaitez tooinclude dans la synchronisation de hello.
2. Pour chaque ajouté et supprimé du domaine, ajuster hello [profils d’exécution](#update-run-profiles).
3. [Appliquer et vérifier les modifications](#apply-and-verify-changes)

### <a name="select-hello-domains-toobe-synchronized"></a>Sélectionnez hello toobe de domaines synchronisé
domaine de hello tooset filtrer, hello comme suit :

1. Connectez-vous au serveur toohello qui exécute la synchronisation Azure AD Connect à l’aide d’un compte qui est membre de hello **ADSyncAdmins** groupe de sécurité.
2. Démarrer **Service de synchronisation** de hello **Démarrer** menu.
3. Sélectionnez **connecteurs**et Bonjour **connecteurs** , sélectionnez hello connecteur avec type de hello **les Services de domaine Active Directory**. Dans **Actions**, sélectionnez**Propriétés**.  
   ![Propriétés du connecteur](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Cliquez sur **Configurer des partitions d’annuaire**.
5. Bonjour **sélectionner les partitions d’annuaire** liste, sélectionner et désélectionner des domaines en fonction des besoins. Vérifiez que les partitions hello uniquement que vous souhaitez toosynchronize sont sélectionnées.  
   ![Partitions](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   Si vous avez modifié votre infrastructure d’Active Directory local et ajouté ou supprimé des domaines de forêt de hello, puis cliquez sur hello **Actualiser** bouton tooget une liste de mises à jour. Lorsque vous actualisez les données, des informations d’identification vous sont demandées. Fournir des informations d’identification avec accès en lecture tooWindows Server Active Directory. Il n’a pas utilisateur hello toobe qui est prérempli dans la boîte de dialogue hello.  
   ![Actualisation requise](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. Lorsque vous avez terminé, fermez hello **propriétés** boîte de dialogue en cliquant sur **OK**. Si vous avez supprimé des domaines à partir de la forêt de hello, un message contextuel indique qu’un domaine a été supprimé et que la configuration est nettoyée.
7. Continuer tooadjust hello [profils d’exécution](#update-run-profiles).

### <a name="update-hello-run-profiles"></a>Mettre à jour les profils hello exécuter
Si vous avez mis à jour votre filtre de domaine, vous devez également des profils de hello exécuter tooupdate.

1. Bonjour **connecteurs** liste, assurez-vous que hello connecteur que vous avez modifié à l’étape précédente de hello est sélectionné. Dans **Actions**, sélectionnez **Configurer des profils d’exécution**.  
   ![Profils d’exécution du connecteur 1](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. Rechercher et identifier hello suivant profils :
    * Importation complète
    * Synchronisation complète
    * Importation d’écart
    * Synchronisation d’écart
    * Exportation
3. Pour chaque profil, ajuster hello **ajouté** et **supprimé** domaines.
    1. Pour chacun des profils de hello cinq, hello comme suit pour chaque **ajouté** domaine :
        1. Sélectionnez le profil de hello exécuter et cliquez sur **nouvelle étape**.
        2. Sur hello **configurer une étape** page hello **Type** menu déroulant, sélectionnez hello type d’étape avec hello même nom que celui que hello du profil que vous configurez. Cliquez ensuite sur **Suivant**.  
        ![Profils d’exécution du connecteur 2](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. Sur hello **Configuration du connecteur** page hello **Partition** menu déroulant, nom sélectionnez hello du domaine hello que vous avez ajouté un filtre de domaine tooyour.  
        ![Profils d’exécution du connecteur 3](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. tooclose hello **configuration du profil exécuter** boîte de dialogue, cliquez sur **Terminer**.
    2. Pour chacun des profils de hello cinq, hello comme suit pour chaque **supprimé** domaine :
        1. Sélectionnez le profil de hello exécuter.
        2. Si hello **valeur** Hello **Partition** attribut est un GUID, hello sélectionnez Exécuter, puis cliquez sur étape **supprimer l’étape**.  
        ![Profils d’exécution du connecteur 4](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. Vérifiez votre modification. Chaque domaine que vous souhaitez toosynchronize doit être répertorié comme une étape dans chaque profil d’exécution.
4. tooclose hello **configurer des profils d’exécution** boîte de dialogue, cliquez sur **OK**.
5.  configuration de hello toocomplete, vous devez toorun une **importation intégrale** et un **synchronisation Delta**. Continuer à lire la section de hello [appliquer et vérifier les modifications](#apply-and-verify-changes).

## <a name="organizational-unitbased-filtering"></a>Filtrage basé sur une unité d’organisation
Hello préféré toochange basée sur l’unité d’organisation de filtrage est en exécutant l’Assistant installation de hello et en modifiant de façon [domaine et le filtrage de l’unité d’organisation](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). l’Assistant installation Hello automatise toutes les tâches de hello sont documentées dans cette rubrique.

Vous devez uniquement suivre ces étapes si vous êtes l’Assistant d’installation ne peut pas toorun hello pour une raison quelconque.

tooconfigure d’organisation unité le filtrage, hello comme suit :

1. Connectez-vous au serveur toohello qui exécute la synchronisation Azure AD Connect à l’aide d’un compte qui est membre de hello **ADSyncAdmins** groupe de sécurité.
2. Démarrer **Service de synchronisation** de hello **Démarrer** menu.
3. Sélectionnez **connecteurs**et Bonjour **connecteurs** , sélectionnez hello connecteur avec type de hello **les Services de domaine Active Directory**. Dans **Actions**, sélectionnez**Propriétés**.  
   ![Propriétés du connecteur](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Cliquez sur **configurer des Partitions d’annuaire**, sélectionnez domaine hello que vous souhaitez tooconfigure, puis cliquez sur **conteneurs**.
5. Lorsque vous y êtes invité, fournissent des informations d’identification avec accès en lecture tooyour sur site Active Directory. Il n’a pas utilisateur hello toobe qui est prérempli dans la boîte de dialogue hello.
6. Bonjour **sélectionner des conteneurs** boîte de dialogue, les unités d’organisation hello clair que vous ne souhaitez toosynchronize à l’annuaire de cloud hello, puis cliquez sur **OK**.  
   ![Unités d’organisation dans la boîte de dialogue Sélectionner des conteneurs hello](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * Hello **ordinateurs** conteneur doit être sélectionné pour votre toobe d’ordinateurs Windows 10 ont bien été synchronisées tooAzure AD. Si les ordinateurs joints à un domaine sont situés dans d’autres unités d’organisation, assurez-vous que ces dernières sont sélectionnées.
   * Hello **ForeignSecurityPrincipals** conteneur doit être sélectionné si vous avez plusieurs forêts avec approbations. Ce conteneur permet de toobe de l’appartenance au groupe de sécurité entre les forêts résolu.
   * Hello **RegisteredDevices** unité d’organisation doit être sélectionnée si vous avez activé la fonctionnalité de l’écriture différée des appareils hello. Si vous utilisez une autre fonction d’écriture différée telle que l’écriture différée de groupe, assurez-vous que ces emplacements sont sélectionnés.
   * Sélectionnez une autre unité d’organisation dans laquelle les utilisateurs, iNetOrgPersons, groupes, contacts et ordinateurs sont localisés. Ces unités d’organisation se trouvent dans une image hello, Bonjour ManagedObjects OU.
   * Si vous utilisez le filtrage basé sur le groupe, hello unité d’organisation où se trouve le groupe de hello doit être inclus.
   * Notez que vous pouvez configurer si les nouvelles unités d’organisation qui sont ajoutées après la configuration de filtrage de hello sont synchronisées ou pas. Consultez la section suivante de hello pour plus d’informations.
7. Lorsque vous avez terminé, fermez hello **propriétés** boîte de dialogue en cliquant sur **OK**.
8. configuration de hello toocomplete, vous devez toorun une **importation intégrale** et un **synchronisation Delta**. Continuer à lire la section de hello [appliquer et vérifier les modifications](#apply-and-verify-changes).

### <a name="synchronize-new-ous"></a>Synchroniser les nouvelles unités d’organisation
Les nouvelles unités d’organisation qui sont créées après la configuration du filtrage sont synchronisées par défaut. Cet état est indiqué par une case cochée. Vous pouvez également désélectionner certaines unités d’organisation secondaires. tooget ce problème, cliquez sur la zone de hello jusqu'à ce qu’il devienne blanc avec une coche bleue (son état par défaut). Puis désélectionnez les sous-unités d’organisation que vous ne souhaitez pas toosynchronize.

Si toutes les unités d’organisation sub sont synchronisées, boîte de hello est blanc avec une coche bleue.  
![Unité d’organisation avec toutes les cases activées](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

Si certains sous-unités d’organisation ont été désélectionnées, boîte de hello est gris avec une coche blanche.  
![Unité d’organisation avec des unités d’organisation secondaires désélectionnées](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

Avec cette configuration, une unité d’organisation qui a été créée sous ManagedObjects est synchronisée.

Assistant d’installation Bonjour Azure AD Connect crée toujours cette configuration.

### <a name="dont-synchronize-new-ous"></a>Ne pas synchroniser les nouvelles unités d’organisation
Vous pouvez configurer la synchronisation de hello moteur toonot synchroniser les nouvelles unités d’organisation issue de la configuration de filtrage de hello. Cet état est indiqué dans hello UI par zone hello apparaissant gris uni avec aucune case à cocher. tooget ce problème, cliquez sur la zone de hello jusqu'à ce qu’il devienne blanc avec aucune case à cocher. Sélectionnez ensuite hello sous-unités d’organisation que vous souhaitez toosynchronize.

![Unité d’organisation avec racine hello non sélectionné](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

Avec cette configuration, une unité d’organisation qui a été créée sous ManagedObjects n’est pas synchronisée.

## <a name="attribute-based-filtering"></a>Filtrage par attribut
Assurez-vous que vous utilisez hello novembre 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) ou version ultérieure de ces étapes toowork.

Le filtrage basé sur l’attribut est objets toofilter moyen plus souples de hello. Vous pouvez utiliser la puissance hello [approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol presque chaque aspect de lorsqu’un objet est synchronisé tooAzure AD.

Vous pouvez appliquer [entrant](#inbound-filtering) le filtrage à partir d’Active Directory toohello métaverse, et [sortant](#outbound-filtering) filtrage de hello métaverse tooAzure AD. Nous vous recommandons d’appliquer le filtrage entrant, car il s’agit de toomaintain plus simple de hello. Vous devez uniquement utiliser le filtrage sortant si toojoin des objets à partir de plusieurs forêts est nécessaire avant l’évaluation hello peut avoir lieu.

### <a name="inbound-filtering"></a>Filtrage entrant
Filtrage entrant utilise la configuration de valeur par défaut de hello, où les objets va tooAzure AD doivent être hello métaverse attribut cloudFiltered ne pas tooa valeur toobe est synchronisé. Si la valeur de cet attribut est défini trop**True**, puis de l’objet de hello n’est pas synchronisé. Il ne doit pas être défini trop**False**, par conception. toomake que les autres règles ont hello capacité toocontribute une valeur, cet attribut est supposé seulement les valeurs de hello toohave **True** ou **NULL** (absent).

Dans le filtrage entrant, vous utilisez power hello de **étendue** toodetermine objets toosynchronize ou pas synchronise. Il s’agit où vous apportez les ajustements toofit propres exigences de votre entreprise. module de portée Hello a un **groupe** et un **clause** toodetermine lorsqu’une règle de synchronisation est dans la portée. Un groupe contient une ou plusieurs clauses. Il existe un « AND » logique entre plusieurs clauses, et un « OR » logique entre plusieurs groupes.

Intéressons-nous à un exemple :   
![Portée](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
Voici la lecture qu’il faut en faire **(service = Informatique) OU (service = Ventes et c = US)**.

Dans hello suivant exemples et les étapes, vous utilisez un objet d’utilisateur hello comme exemple, mais vous pouvez l’utiliser pour tous les types d’objet.

Bonjour suivant des exemples, valeur de priorité hello commence à 50. Il peut s’agir de n’importe quel nombre non utilisé, mais la valeur doit être inférieure à 100.

#### <a name="negative-filtering-do-not-sync-these"></a>Filtrage négatif : « ne pas synchroniser »
Dans l’exemple suivant de hello, vous exclure (pas synchroniser) tous les utilisateurs où **extensionAttribute15** a la valeur de hello **NoSync**.

1. Connectez-vous au serveur toohello qui exécute la synchronisation Azure AD Connect à l’aide d’un compte qui est membre de hello **ADSyncAdmins** groupe de sécurité.
2. Démarrer **Éditeur des règles de synchronisation** de hello **Démarrer** menu.
3. Assurez-vous que l’option **Entrante** est sélectionnée, puis cliquez sur **Ajouter une nouvelle règle**.
4. Donnez à hello règle un nom descriptif, tel que «*dans à partir d’AD-User Filtredonotsync*». Forêt appropriée de sélectionnez hello, sélectionnez **utilisateur** comme hello **type d’objet CS**, puis sélectionnez **personne** comme hello **type d’objet MV**. Dans **Type de lien**, sélectionnez **Jointure**. Dans la zone **Précédence**, tapez une valeur actuellement non utilisée par une autre règle de synchronisation (par exemple, 50), puis cliquez sur **Suivant**.  
   ![1 description entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. Dans la zone **Filtre d’étendue**, cliquez sur **Ajouter un groupe**, puis sur **Ajouter une clause**. Dans la zone **Attribut**, sélectionnez **ExtensionAttribute15**. Assurez-vous que **opérateur** est défini trop**égal**et tapez Bonjour valeur **NoSync** Bonjour **valeur** boîte. Cliquez sur **Suivant**.  
   ![2 étendue entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Laissez hello **joindre** règles vide, puis cliquez sur **suivant**.
7. Cliquez sur **ajouter une Transformation**, sélectionnez hello **FlowType** en tant que **constante**, puis sélectionnez **cloudFiltered** comme hello  **Cible d’attribut**. Bonjour **Source** zone de texte, tapez **True**. Cliquez sur **ajouter** règle de hello toosave.  
   ![3 transformation entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. configuration de hello toocomplete, vous devez toorun une **une synchronisation complète**. Continuer à lire la section de hello [appliquer et vérifier les modifications](#apply-and-verify-changes).

#### <a name="positive-filtering-only-sync-these"></a>Filtrage positif : « synchroniser uniquement ces éléments »
Expression de filtrage positif peut être plus difficile, car vous avez également tooconsider les objets qui ne sont pas évident toobe synchronisée, comme les salles de conférence. Vous êtes également filtre par défaut de cours toooverride hello dans la règle d’out-of-box hello **dans depuis AD - jointure utilisateur**. Lorsque vous créez votre filtre personnalisé, assurez-vous que toonot incluent des objets système critiques, objets de conflits de réplication, des boîtes aux lettres spéciaux et les comptes de service hello pour Azure AD Connect.

option de filtrage positif Hello requiert deux règles de synchronisation. Vous avez besoin d’une règle (ou plusieurs) avec la portée correcte de hello d’objets toosynchronize. ainsi qu’une deuxième règle de synchronisation fourre-tout excluant tous les objets qui n’ont pas encore été identifiés en tant qu’objets à synchroniser.

Dans l’exemple suivant de hello, vous synchronisez uniquement les objets utilisateur où hello département de l’attribut est hello **Sales**.

1. Connectez-vous au serveur toohello qui exécute la synchronisation Azure AD Connect à l’aide d’un compte qui est membre de hello **ADSyncAdmins** groupe de sécurité.
2. Démarrer **Éditeur des règles de synchronisation** de hello **Démarrer** menu.
3. Assurez-vous que l’option **Entrante** est sélectionnée, puis cliquez sur **Ajouter une nouvelle règle**.
4. Donnez à hello règle un nom descriptif, tel que «*depuis AD-utilisateur ventes synchronisés*». Forêt appropriée de sélectionnez hello, sélectionnez **utilisateur** comme hello **type d’objet CS**, puis sélectionnez **personne** comme hello **type d’objet MV**. Dans **Type de lien**, sélectionnez **Jointure**. Dans la zone **Précédence**, tapez une valeur actuellement non utilisée par une autre règle de synchronisation (par exemple, 51), puis cliquez sur **Suivant**.  
   ![4 description entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. Dans la zone **Filtre d’étendue**, cliquez sur **Ajouter un groupe**, puis sur **Ajouter une clause**. Dans la zone **Attribut**, sélectionnez **department**. Assurez-vous qu’opérateur est défini trop**égal**et tapez Bonjour valeur **Sales** Bonjour **valeur** boîte. Cliquez sur **Suivant**.  
   ![5 étendue entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Laissez hello **joindre** règles vide, puis cliquez sur **suivant**.
7. Cliquez sur **ajouter une Transformation**, sélectionnez **constante** comme hello **FlowType**et sélectionnez hello **cloudFiltered** comme hello  **Cible d’attribut**. Bonjour **Source** , tapez **False**. Cliquez sur **ajouter** règle de hello toosave.  
   ![6 transformation entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   Il s’agit d’un cas particulier où vous définissez explicitement cloudFiltered trop**False**.
8. Nous disposons de la règle de synchronisation de fourre-tout toocreate hello. Donnez à hello règle un nom descriptif, tel que «*dans depuis AD-filtre d’utilisateur fourre-tout*». Forêt appropriée de sélectionnez hello, sélectionnez **utilisateur** comme hello **type d’objet CS**, puis sélectionnez **personne** comme hello **type d’objet MV**. Dans **Type de lien**, sélectionnez **Jointure**. Dans la zone **Précédence**, tapez une valeur actuellement non utilisée par une autre règle de synchronisation (par exemple, 99). Vous avez sélectionné une valeur de priorité est plus élevée (priorité inférieure) à celle de la règle de synchronisation précédente hello. Mais vous avez également espace afin que vous pouvez ajouter plusieurs règles de filtrage de synchronisation ultérieurement lorsque vous souhaitez toostart synchronisation des services supplémentaires. Cliquez sur **Suivant**.  
   ![7 description entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. Laissez l’option **Filtre d’étendue** vide, puis cliquez sur **Suivant**. Un filtre vide indique que cette règle hello est toobe appliqué tooall objets.
10. Laissez hello **joindre** règles vide, puis cliquez sur **suivant**.
11. Cliquez sur **ajouter une Transformation**, sélectionnez **constante** comme hello **FlowType**, puis sélectionnez **cloudFiltered** comme hello  **Cible d’attribut**. Bonjour **Source** , tapez **True**. Cliquez sur **ajouter** règle de hello toosave.  
    ![3 transformation entrante](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. configuration de hello toocomplete, vous devez toorun une **une synchronisation complète**. Continuer à lire la section de hello [appliquer et vérifier les modifications](#apply-and-verify-changes).

Si vous le souhaitez, vous pouvez créer plusieurs règles de type de première hello inclut plusieurs objets dans la synchronisation de hello.

### <a name="outbound-filtering"></a>Filtrage sortant
Dans certains cas, il est hello toodo nécessaire le filtrage uniquement une fois que les objets hello ont été joints dans le métaverse de hello. Par exemple, il peut être nécessaire toolook à l’attribut de messagerie hello à partir de la forêt de ressources hello et attribut userPrincipalName de hello de forêt de comptes hello, toodetermine si un objet doit être synchronisé. Dans ces cas, vous créez hello filtrage sur une règle de trafic sortant hello.

Dans cet exemple, vous modifiez hello filtrées afin que seuls les utilisateurs qui ont leur messagerie et l’userPrincipalName se terminant par @contoso.com sont synchronisés :

1. Connectez-vous au serveur toohello qui exécute la synchronisation Azure AD Connect à l’aide d’un compte qui est membre de hello **ADSyncAdmins** groupe de sécurité.
2. Démarrer **Éditeur des règles de synchronisation** de hello **Démarrer** menu.
3. Sous **Type de règles**, cliquez sur **Sortant**.
4. Règle de hello rechercher nommée **hors tooAAD – User Join**, puis cliquez sur **modifier**.
5. Dans la fenêtre contextuelle hello, répondre **Oui** toocreate une copie de la règle de hello.
6. Sur hello **Description** , changez **priorité** tooan valeur inutilisé, par exemple 50.
7. Cliquez sur **Scoping filter** sur hello de navigation de gauche, puis cliquez sur **clause Add**. Dans la zone **Attribut**, sélectionnez **mail**. Dans la zone **Opérateur**, sélectionnez **ENDSWITH**. Dans la zone **Valeur**, tapez **@contoso.com**, puis cliquez sur **Ajouter une clause**. Dans la zone **Attribut**, sélectionnez **userPrincipalName**. Dans la zone **Opérateur**, sélectionnez **ENDSWITH**. Dans la zone **Valeur**, tapez **@contoso.com**.
8. Cliquez sur **Enregistrer**.
9. configuration de hello toocomplete, vous devez toorun une **une synchronisation complète**. Continuer à lire la section de hello [appliquer et vérifier les modifications](#apply-and-verify-changes).

## <a name="apply-and-verify-changes"></a>Appliquer et vérifier les modifications
Une fois que vous avez modifié votre configuration, vous devez appliquer les toohello les objets qui sont déjà présents dans le système de hello. Il peut être également que les objets hello qui ne sont pas actuellement dans le moteur de synchronisation hello doivent être traités (moteur de synchronisation hello doit système source de hello tooread tooverify à nouveau son contenu).

Si vous avez modifié la configuration de hello à l’aide de **domaine** ou **-unité d’organisation** le filtrage, vous devez toodo une **importation intégrale**, suivi par **Delta synchronisation**.

Si vous avez modifié la configuration de hello à l’aide de **attribut** le filtrage, vous devez toodo une **synchronisation complète**.

Hello comme suit :

1. Démarrer **Service de synchronisation** de hello **Démarrer** menu.
2. Sélectionnez **Connecteurs**. Bonjour **connecteurs** , sélectionnez hello connecteur où vous avez effectué une configuration modifier précédemment. Dans **Actions**, sélectionnez **Exécuter**.  
   ![Exécution de connecteur](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. Dans **profils d’exécution**, sélectionnez l’opération hello mentionné dans la section précédente de hello. Si vous avez besoin de toorun deux actions, exécution hello seconde après hello première soit terminée. (hello **état** colonne est **inactif** pour le connecteur de hello sélectionné.)

Après la synchronisation de hello, toutes les modifications sont mises en lots toobe exporté. Avant d’apporter réellement des modifications de hello dans Azure AD, vous souhaitez tooverify que toutes ces modifications sont correctes.

1. Démarrez une invite de commandes et accédez trop`%Program Files%\Microsoft Azure AD Sync\bin`.
2. Exécutez `csexport "Name of Connector" %temp%\export.xml /f:x`.  
   nom Hello Hello connecteur est le Service de synchronisation. Il a un too"contoso.com similaire nom – AAD » pour Azure AD.
3. Exécutez `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv`.
4. Vous disposez maintenant d’un fichier dans %temp% nommé export.csv qui peuvent être examiné dans Microsoft Excel. Ce fichier contient toutes les modifications hello sur toobe exporté.
5. Apporter les modifications nécessaires hello toohello données ou la configuration et exécuter ces étapes à nouveau (importation, synchroniser et vérifiez) jusqu'à ce que hello modifications concernent toobe exporté correspondent à vos attentes.

Lorsque vous êtes satisfait, exportez hello modifications tooAzure AD.

1. Sélectionnez **Connecteurs**. Bonjour **connecteurs** , sélectionnez hello connecteur Azure AD. Dans **Actions**, sélectionnez **Exécuter**.
2. Dans **Profils d’exécution**, sélectionnez **Exporter**.
3. Si vos modifications de configuration supprimer plusieurs objets, vous verrez une erreur dans l’exportation de hello lorsque le nombre de hello est supérieure au seuil hello configuré (par défaut 500). Si vous recevez cette erreur, vous devez tootemporarily désactiver hello »[empêcher des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)« fonctionnalité.

Il est désormais à nouveau Planificateur de temps tooenable hello.

1. Démarrer **du Planificateur de tâches** de hello **Démarrer** menu.
2. Directement sous **bibliothèque du Planificateur de tâches**, tâche hello de recherche nommé **Azure AD Sync Scheduler**, avec le bouton droit, puis sélectionnez **activer**.

## <a name="group-based-filtering"></a>Filtrage de groupe
Vous pouvez configurer basée sur le groupe de filtrage hello première fois que vous installez Azure AD Connect à l’aide de [installation personnalisée](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups). Son destinés à un déploiement pilote où vous souhaitez uniquement un petit ensemble de toobe objets synchronisé. Lorsque vous désactivez le filtrage basé sur un groupe, vous ne pouvez plus le réactiver. Il a *ne pas pris en charge* toouse basé le filtrage dans une configuration personnalisée. Il est uniquement pris en charge tooconfigure cette fonctionnalité à l’aide de l’Assistant installation hello. Lorsque vous avez terminé votre projet pilote, puis utilisez une de hello autres options de filtrage dans cette rubrique. Lorsque vous utilisez basée sur une unité d’organisation filtrage conjointement avec le filtrage basé sur le groupe, hello OU(s) où se trouvent les groupe hello et ses membres doit être inclus.

Lors de la synchronisation de plusieurs forêts Active Directory, vous pouvez configurer le filtrage basé sur les groupes en spécifiant un groupe différent pour chaque connecteur Active Directory. Si vous le souhaitez toosynchronize un utilisateur dans une forêt Active Directory et hello même utilisateur dispose d’une ou plus correspondant FSP (entité de sécurité externe) des objets dans d’autres forêts Active Directory, vous devez vous assurer que cet objet utilisateur hello et tous les correspondants FSP situent les objets basée sur un groupe filtrage de l’étendue. Si une ou plusieurs des objets FSP hello sont exclus par filtrage basé sur le groupe, objet utilisateur de hello ne sera pas synchronisé tooAzure AD.

## <a name="next-steps"></a>Étapes suivantes
- Apprenez-en davantage sur la configuration de la [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md).
- Apprenez-en davantage sur [l’intégration de vos identités locales à Azure AD](active-directory-aadconnect.md).
