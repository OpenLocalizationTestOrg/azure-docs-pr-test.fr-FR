---
title: 'Synchronisation Azure AD Connect : Apporter une modification dans la synchronisation Azure AD Connect | Microsoft Docs'
description: Vous guide dans toomake une toohello modifier la configuration dans Azure AD Connect de la synchronisation.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Synchronisation Azure AD Connect : comment toomake un toohello de modification de configuration par défaut
Hello cette rubrique vise toowalk vous guide dans la façon dont toomake modifie la configuration par défaut de toohello de synchronisation Azure AD Connect. Elle explique pas à pas la procédure pour les scénarios courants. Sachant cela, vous devez être en mesure de toomake tooyour de certaines modifications simples possèdent la configuration en fonction de vos propres règles d’entreprise.

## <a name="synchronization-rules-editor"></a>Éditeur de règles de synchronisation
Hello Éditeur des règles de synchronisation est utilisée configuration par défaut hello toosee et de modification. Vous pouvez le trouver dans le Menu Démarrer de hello sous hello **Azure AD Connect** groupe.  
![Menu Démarrer avec l’Éditeur de règles de synchronisation](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

Lorsque vous l’ouvrez, vous voyez des règles d’out-of-box hello par défaut.

![Éditeur de règles de synchronisation](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Navigation dans l’éditeur de hello
listes déroulantes Hello haut hello de l’éditeur de hello autoriser tooquickly rechercher une règle particulière. Par exemple, si vous souhaitez que les règles de hello toosee où hello attribut proxyAddresses est inclus, vous modifieriez suivant de toohello les zones déroulantes hello :  
![Filtrage SRE](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
tooreset le filtrage et la charge d’une nouvelle configuration, appuyez sur **F5** clavier de hello.

toohello droite en haut, vous disposez d’un bouton **ajouter une nouvelle règle**. Ce bouton est toocreate utilisé votre propre règle personnalisée.

Au bas de hello, vous disposez des boutons d’action sur une règle de synchronisation sélectionné. Les boutons **Modifier** et **Supprimer** permettent de modifier et de supprimer des règles. **Exporter** génère un script PowerShell pour recréer la règle de synchronisation hello. Cette procédure vous permet de toomove une règle de synchronisation à partir d’un serveur tooanother.

## <a name="create-your-first-custom-rule"></a>Création de votre première règle personnalisée
changement le plus courant Hello est un flux d’attributs de toohello de modifications. les données de salutation dans votre répertoire source peut-être pas comme dans Azure AD. Dans l’exemple hello dans cette section, vous souhaitez toomake que hello nom donné à un utilisateur est toujours en **majuscules**.

### <a name="disable-hello-scheduler"></a>Désactiver le Planificateur de hello
Hello [planificateur](active-directory-aadconnectsync-feature-scheduler.md) s’exécute toutes les 30 minutes par défaut. Vous souhaitez toomake qu’il ne démarre pas pendant que vous apportez des modifications et résoudre les problèmes de vos nouvelles règles. tootemporarily désactive hello planificateur, démarrez PowerShell et exécutez`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Désactiver le Planificateur de hello](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Créer la règle de hello
1. Cliquez sur **Ajouter une nouvelle règle**.
2. Sur hello **Description** page entrez hello qui suit :  
   ![Filtrage des règles entrantes](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * Nom : Donner un nom descriptif à la règle de hello.
   * Description : Une explication pour une autre personne peut comprendre quelle règle hello concerne.
   * Connecté système : objet de hello hello système sont accessibles. Dans ce cas, sélectionnez hello connecteur Active Directory.
   * Connected System/Metaverse Object Type (Type de système connecté/d’objet métaverse) : sélectionnez **Utilisateur** et **Personne**, respectivement.
   * Le Type de lien : Cette valeur est également modifier**joindre**.
   * Priorité : Fournir une valeur qui est unique dans le système de hello. Une valeur numérique inférieure indique une priorité plus élevée.
   * Balise : laissez ce champ vide. Seules les règles par défaut de Microsoft doivent contenir une valeur dans cette zone.
3. Sur hello **Scoping filter** , entrez **givenName ISNOTNULL**.  
   ![Filtre d’étendue des règles entrantes](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   Cette section est utilisé toodefine la règle de hello objets doit s’appliquer. Si vide, la règle de hello appliquerait tooall objets de l’utilisateur. y compris les salles de conférence, les comptes de service et les autres objets d’utilisateurs non humains.
4. Sur hello **règles de jointure**, laissez vide.
5. Sur hello **Transformations** , changez hello FlowType trop**Expression**. Sélectionnez hello attribut cible **givenName**et entrez dans la Source `PCase([givenName])`.
   ![Transformations des règles entrantes](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   moteur de synchronisation Hello respecte la casse dans le nom de la fonction hello et nom hello d’attribut de hello. Si vous tapez un problème, vous consultez un avertissement lorsque vous ajoutez des règles de hello. éditeur de Hello vous permet de toosave et continuer, donc vous devez tooreopen hello règle et hello correct.
6. Cliquez sur **ajouter** règle de hello toosave.

Votre nouvelle règle personnalisée doit être visible par hello autres règles de synchronisation dans un système de hello.

### <a name="verify-hello-change"></a>Vérifiez le changement de hello
Avec cette modification, vous souhaitez toomake qu’il fonctionne comme prévu et n’est pas lever des erreurs. En fonction du nombre hello d’objets que vous avez, existe deux façons différentes toodo cette étape.

1. Exécuter une synchronisation complète de tous les objets
2. Exécuter un aperçu et une synchronisation complète sur un seul objet

Démarrer **Service de synchronisation** à partir du menu Démarrer de hello. étapes de Hello dans cette section sont tous dans cet outil.

1. **Synchronisation complète de tous les objets**  
   Sélectionnez **connecteurs** haut hello. Identifier hello connecteur que vous avez apportées à une section précédente de modification tooin hello, dans ce cas hello des Services de domaine Active Directory et sélectionnez-le. Sous Actions, sélectionnez **Exécuter**, puis **Synchronisation complète** et **OK**.
   ![Synchronisation complète](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   Hello objets sont désormais mis à jour dans le métaverse de hello. Vous souhaitez maintenant toolook objet hello hello métaverse.
2. **Aperçu et synchronisation complète d’un seul objet**  
   Sélectionnez **connecteurs** haut hello. Identifier hello connecteur que vous avez apportées à une section précédente de modification tooin hello, dans ce cas hello des Services de domaine Active Directory et sélectionnez-le. Sélectionnez **Search Connector Space**(Rechercher l’espace de connecteur). Utilisez l’étendue toofind un objet que vous souhaitez toouse tootest hello modification. Sélectionnez l’objet de hello et cliquez sur **aperçu**. Dans un nouvel écran hello, sélectionnez **valider la version préliminaire**.  
   ![Commit preview](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   Hello changement est maintenant validée toohello métaverse.

**Examiner les objet hello hello métaverse**  
Vous souhaitez maintenant toopick que quelques objets toomake vraiment hello valeur d’exemple est prévu et cette règle hello appliquée. Sélectionnez **recherche de métaverse** à partir du haut de hello. Ajoutez tout filtre que vous avez besoin d’objets toofind hello. À partir du résultat de recherche hello, ouvrez un objet. Examinez les valeurs d’attribut hello et également vérifier Bonjour **règles de synchronisation** colonne hello règle appliquée comme prévu.  
![Metaverse search](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Activer le Planificateur de hello
Si tout est comme prévu, vous pouvez activer le planificateur hello à nouveau. À partir de PowerShell, exécutez `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="other-common-attribute-flow-changes"></a>Autres modifications courantes du flux d’attributs
section précédente de Hello décrit comment toomake modifie le flux d’attribut tooan. Dans cette section, vous trouverez d’autres exemples. étapes Hello pour la règle de synchronisation toocreate hello est abrégée, mais vous trouverez hello complète dans la section précédente de hello.

### <a name="use-another-attribute-than-hello-default"></a>Utiliser un autre attribut à valeur par défaut de hello
Chez Fabrikam, est une forêt où alphabet local de hello est utilisé pour le nom donné, prénom et nom d’affichage. Hello représentation sous forme de caractères latins de ces attributs sont accessibles dans les attributs d’extension hello. Lors de la génération de liste d’adresses globale hello dans Azure AD et Office 365, l’organisation de hello veut ces toobe attributs utilisé à la place.

Avec une configuration par défaut, un objet à partir de la forêt locale de hello ressemble à ceci :  
![Flux d’attributs 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

toocreate une règle avec d’autres flux d’attribut, hello suivant :

* Démarrer **éditeur de règles de synchronisation** à partir du menu Démarrer de hello.
* Avec **entrant** toohello encore sélectionné de gauche, cliquez sur le bouton de hello **ajouter une nouvelle règle**.
* Donnez à la règle de hello un nom et une description. Sélectionnez hello locale Active Directory et hello applique les types d’objets. Dans **Type de lien**, sélectionnez **Jointure**. Pour le choix de la priorité, sélectionnez un nombre qui n’est pas utilisé par une autre règle. règles d’out-of-box Hello commencent par 100, donc la valeur de hello 50 peut être utilisée dans cet exemple.
  ![Flux d’attributs 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* Ne renseignez pas étendue (autrement dit, doit s’appliquer tooall les objets utilisateur dans la forêt de hello).
* Laissez les règles de jointure vides (qui est, permettent de hello handle de la règle d’out-of-box toutes les jointures).
* Dans les Transformations, créer hello suivant du flux :  
  ![Flux d’attributs 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* Cliquez sur **ajouter** règle de hello toosave.
* Accédez trop**Synchronization Service Manager**. Sur **connecteurs**, sélectionnez hello connecteur où nous avons ajouté la règle de hello. Sélectionnez **Exécuter** et **Synchronisation complète**. Une synchronisation complète recalcule tous les objets à l’aide de règles en cours de hello.

Il s’agit de résultat de hello pour hello même de l’objet avec cette règle personnalisée :  
![Flux d’attributs 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>Longueur des attributs
Attributs de chaîne sont par toobe de jeu par défaut indexable et la longueur maximale hello est de 448 caractères. Si vous travaillez avec des attributs de chaîne qui peuvent contenir plusieurs, puis apportez suivant de hello tooinclude que dans le flux d’attribut hello :  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>La modification hello userPrincipalSuffix
attribut userPrincipalName de Hello dans Active Directory n’est pas toujours connu par les utilisateurs de hello et peut ne pas convenir comme hello nom de connexion. Bonjour Azure AD Connect Assistant installation de la synchronisation permet de choisir un autre attribut, par exemple les messages de. Mais dans certains hello cas l’attribut doit être calculé. Par exemple, l’entreprise hello Contoso a deux annuaires Azure AD, un pour la production et un pour le test. Ils veulent utilisateurs hello dans leur test locataire toouse un autre suffixe hello nom de connexion.  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

Dans cette expression, prennent tout à gauche de hello tout d’abord @-sign (Word) et le concatène avec une chaîne fixe.

### <a name="convert-a-multi-value-tooa-single-value"></a>Convertir une valeur unique à valeurs multiples tooa
Certains attributs dans Active Directory sont à valeurs multiples dans le schéma de hello même s’ils ressemblent uniques de valeur dans les ordinateurs et utilisateurs Active Directory. Un exemple est l’attribut de description hello.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

Dans cette expression au cas où l’attribut de hello a une valeur, de prendre le premier élément de hello (élément) dans l’attribut de hello, supprimer les espaces à gauche et (Trim), et puis conserver hello 448 premiers caractères (à gauche) dans la chaîne de hello.

### <a name="do-not-flow-an-attribute"></a>Ne transmettez pas d'attribut
Pour plus d’informations sur le scénario hello pour cette section, consultez [contrôler le processus de flux d’attribut hello](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).

Il existe deux façons toonot flux un attribut. tout d’abord, Hello est disponible dans l’Assistant installation hello et vous permet de trop[supprimer les attributs sélectionnés](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering). Cette option fonctionne si vous n’avez jamais synchronisé attribut hello avant. Toutefois, si vous avez démarré toosynchronize cet attribut et le supprimez ultérieurement avec cette fonctionnalité, moteur de synchronisation hello arrête la gestion des attributs de hello et les valeurs existantes hello sont laissés dans Azure AD.

Si vous que tooremove hello la valeur d’un attribut et assurez-vous qu’il ne transmet pas Bonjour futures, vous devez créer une règle personnalisée à la place.

Chez Fabrikam, nous avons réalisé que certains hello attributs nous synchroniser toohello cloud ne doivent pas exister. Nous souhaitons toomake que ces attributs sont supprimés d’Azure AD.  
![Attributs d’extension erronés](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* Créer une nouvelle règle de synchronisation entrants et remplir la description de hello ![Descriptions](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* Créer des flux d’attributs de type **Expression** et avec une source de hello **AuthoritativeNull**. Hello littéral **AuthoritativeNull** indique que la valeur de hello doit être vide dans hello MV même si la valeur de hello toopopulate tente d’une règle de synchronisation de priorité inférieure.
  ![Transformation des attributs d’extension](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Enregistrer la règle de synchronisation de hello. Démarrer **Service de synchronisation**, recherche hello connecteur, sélectionnez **exécuter**, et **synchronisation complète**. Cette étape permet de recalculer tous les flux d’attributs.
* Vérifiez que hello destiné modifications concernent toobe exporté en recherchant l’espace de connecteur hello.
  ![Suppression progressive](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>Création de règles avec PowerShell
À l’aide d’éditeur de règles de synchronisation hello fonctionne correctement lorsque vous avez seulement quelques modifications toomake. Si vous devez toomake de nombreuses modifications, PowerShell peut être une meilleure option. Certaines fonctionnalités avancées sont uniquement disponibles avec PowerShell.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Obtenir un script PowerShell de hello pour une règle d’out-of-box
éditeur, cliquez sur les règles toosee hello script PowerShell qui a créé une règle d’out-of-box, une règle de sélection hello dans synchronisation des hello **exporter**. Cette règle hello créé un script ainsi action hello de PowerShell.

### <a name="advanced-precedence"></a>Priorité avancée
règles de synchronisation d’out-of-box Hello commencent par une valeur de priorité de 100. Si vous avez plusieurs forêts et que vous devez toomake nombreuses modifications personnalisées, puis les règles de synchronisation 99 peuvent ne pas suffire.

Vous pouvez demander à hello moteur de synchronisation que vous souhaitez que les règles supplémentaires insérés avant les règles d’out-of-box hello. tooget ce problème, procédez comme suit :

1. La règle de synchronisation d’out-of-box première marque hello (cette règle est hello **dans à partir de la jointure AD-utilisateur**) dans l’éditeur de règles de synchronisation hello et sélectionnez **exporter**. Copier la valeur de l’identificateur de SR hello.  
![PowerShell avant modification](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Créer la nouvelle règle de synchronisation hello. Vous pouvez utiliser toocreate de l’éditeur de règle de synchronisation hello il. Exporter le script PowerShell de hello règle tooa.
3. Dans la propriété de hello **PrecedenceBefore**, insérez la valeur de l’identificateur hello à partir de la règle d’out-of-box hello. Ensemble hello **priorité** trop**0**. Assurez-vous d’un attribut d’identificateur hello est unique et vous ne réutilisez pas un GUID à partir d’une autre règle. Assurez-vous également que hello **ImmutableTag** propriété n’est pas définie, cette propriété doit uniquement être définie pour une règle d’out-of-box. Enregistrer le script PowerShell de hello et exécutez-le. résultat de Hello est que votre règle personnalisée est affectée à hello priorité 100 et toutes les autres règles out-of-box sont incrémentés.  
![PowerShell après modification](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

Vous pouvez avoir plusieurs règles de synchronisation personnalisées à l’aide de hello même **PrecedenceBefore** valeur si nécessaire.


## <a name="enable-synchronization-of-preferreddatalocation"></a>Activer la synchronisation de l’attribut PreferredDataLocation
Azure AD Connect prend en charge la synchronisation de hello **PreferredDataLocation** attribut **utilisateur** objets dans la version 1.1.524.0 et après. Plus spécifiquement, les modifications introduites sont les suivantes :

* schéma Hello hello du type d’objet **utilisateur** Bonjour Azure le connecteur Active Directory est étendu tooinclude PreferredDataLocation attribut, qui est de type chaîne et est à valeur unique.

* schéma Hello hello du type d’objet **personne** Bonjour métaverse est étendu tooinclude PreferredDataLocation attribut, qui est de type chaîne et est à valeur unique.

Par défaut, attribut de PreferredDataLocation hello n’est pas activé pour la synchronisation, car il n’existe aucun attribut PreferredDataLocation correspondant dans Active Directory local. Vous devez activer manuellement la synchronisation.

> [!IMPORTANT]
> Actuellement, Azure AD autorise un attribut de PreferredDataLocation hello sur des objets utilisateur synchronisé et cloud toobe d’objets utilisateur directement configuré à l’aide de PowerShell Azure AD. Une fois que vous avez activé la synchronisation de l’attribut de PreferredDataLocation hello, vous devez arrêter l’aide de PowerShell Azure AD tooconfigure hello attribut **synchronisée d’objets utilisateur** comme Azure AD Connect remplace selon leur valeurs d’attribut source Hello dans Active Directory local.

> [!IMPORTANT]
> Sur 2017 1 de septembre, Azure AD n’autorise plus attribut PreferredDataLocation de hello sur **synchronisée d’objets utilisateur** toobe directement configuré à l’aide de PowerShell Azure AD. l’attribut PreferredLocation tooconfigure sur synchronisé les objets utilisateur, vous devez utiliser Azure AD Connect uniquement.

Avant d’activer la synchronisation de l’attribut de PreferredDataLocation hello, procédez comme suit :

 * Tout d’abord, déterminez quels toobe d’attribut Active Directory local utilisé comme attribut de source de hello. Il doit être de type **chaîne** et **à valeur unique**.

 * Si vous avez déjà configuré l’attribut de PreferredDataLocation hello sur existant synchronisé des objets utilisateur dans Azure AD à l’aide d’Azure AD PowerShell, vous devez **backport** toohello les objets utilisateur correspondants des valeurs d’attributs de hello dans l’annuaire local.
 
    > [!IMPORTANT]
    > Si vous le faites pas backport hello attribut valeurs toohello objets utilisateur correspondants dans Active Directory local, Azure AD Connect supprimera les valeurs d’attribut existantes hello dans Azure AD lorsque la synchronisation pour l’attribut de PreferredDataLocation hello est activé.

 * Il est recommandé de configurer d’attribut de source de hello au moins deux local utilisateur AD objets maintenant, qui peut être utilisé pour la vérification de version ultérieure.
 
synchronisation de tooenable Hello étapes de l’attribut de PreferredDataLocation hello peut se résumer ainsi :

1. Désactiver le planificateur de synchronisation et vérifier qu'aucune synchronisation n’est en cours

2. Ajouter hello source attribut toohello AD connecteur local schéma

3. Ajouter un schéma de connecteur Azure AD PreferredDataLocation toohello

4. Créer une valeur d’attribut de synchronisation entrante règle tooflow hello à partir d’Active Directory local

5. Créer un attribut valeur tooAzure AD synchronisation sortante règle tooflow hello

6. Exécuter un cycle de synchronisation complète

7. Activer le planificateur de synchronisation

> [!NOTE]
> reste Hello de cette section couvre les étapes suivantes dans les détails. Ils sont décrits dans le contexte hello d’un déploiement d’Azure AD avec la topologie de forêt unique et sans règles de synchronisation personnalisées. Si vous avez plusieurs forêts topologie, les règles de synchronisation personnalisé configuré ou disposer d’un serveur intermédiaire, vous devez les étapes de hello tooadjust en conséquence.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Étape 1 : désactiver le planificateur de synchronisation et vérifier qu’aucune synchronisation n’est en cours
Vérifiez aucune synchronisation n’a lieu lorsque vous vous trouvez au milieu de hello de mise à jour de la synchronisation tooavoid règles involontaire change étant exportés tooAzure AD. Planificateur de synchronisation intégré toodisable hello :

 1. Démarrez la session PowerShell sur le serveur d’Azure AD Connect hello.

 2. Désactivez la synchronisation planifiée en exécutant l’applet de commande : `Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Démarrer hello **Synchronization Service Manager** par → de tooSTART va Service de synchronisation.
 
 4. Accédez toohello **Operations** onglet et confirmer aucune opération dont le statut est *« en cours. »*

![Synchronization Service Manager - Vérifier qu’aucune opération n’est en cours](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>Étape 2 : Ajouter hello source attribut toohello AD connecteur local schéma
Pas tous les attributs AD sont importés dans hello espace de connecteur Active Directory sur site. liste tooadd hello source attribut toohello Hello importés des attributs :

 1. Accédez toohello **connecteurs** onglet Bonjour Synchronization Service Manager.
 
 2. Avec le bouton droit sur hello **le connecteur Active Directory local** et sélectionnez **propriétés**.
 
 3. Dans la boîte de dialogue contextuelle hello, accédez toohello **sélectionner les attributs** onglet.
 
 4. Vérifiez que hello source est cochée dans la liste d’attributs hello.
 
 5. Cliquez sur **OK** toosave.

![Ajouter le site source attribut tooon schéma de connecteur AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>Étape 3 : Ajouter des schémas de connecteur Azure AD PreferredDataLocation toohello
Par défaut, l’attribut de PreferredDataLocation de hello n’est pas importé dans hello espace de connexion Azure AD. tooadd hello PreferredDataLocation attribut toohello liste des attributs importés :

 1. Accédez toohello **connecteurs** onglet Bonjour Synchronization Service Manager.

 2. Avec le bouton droit sur hello **connecteur Azure AD** et sélectionnez **propriétés**.

 3. Dans la boîte de dialogue contextuelle hello, accédez toohello **sélectionner les attributs** onglet.

 4. Vérifiez que hello PreferredDataLocation case est cochée dans la liste d’attributs hello.

 5. Cliquez sur **OK** toosave.

![Ajouter l’attribut de source tooAzure schéma de connecteur AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>Étape 4 : Créer une valeur d’attribut de synchronisation entrante règle tooflow hello à partir d’Active Directory local
règle de synchronisation entrante Hello permet tooflow de valeur d’attribut hello à partir de l’attribut source locale Active Directory toohello métaverse hello :

1. Démarrer hello **Éditeur des règles de synchronisation** par → de tooSTART va synchronisation éditeur de règles.

2. Définir un filtre de recherche hello **Direction** toobe **entrant**.

3. Cliquez sur **ajouter une nouvelle règle** bouton toocreate une règle de trafic entrant.

4. Sous hello **Description** , onglet de fournir hello configuration suivante :
 
    | Attribut | Valeur | Détails |
    | --- | --- | --- |
    | Nom | *Donnez-lui un nom* | Par exemple, *« Entrant depuis AD – Utilisateur PreferredDataLocation”* |
    | Description | *Fournissez une description* |  |
    | Système connecté | *Choisissez hello localement le connecteur Active Directory* |  |
    | Type d’objet système connecté | **Utilisateur** |  |
    | Type d’objet Metaverse | **Person** |  |
    | Type de lien | **Join** |  |
    | Precedence | *Choisissez une valeur comprise entre 1 et 99* | Les valeurs de 1 à 99 sont réservées aux règles de synchronisation personnalisées. Ne sélectionnez pas de valeur utilisée par une autre règle de synchronisation. |

5. Accédez toohello **Scoping filter** onglet et ajouter un **unique groupe de filtres étendue avec hello suivant clause**:
 
    | Attribut | Opérateur  | Valeur |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | Utilisateur\_ | 
 
    Le filtre d’étendue détermine les objets de l’Active Directory local auxquels cette règle de synchronisation de trafic entrant s’applique. Dans cet exemple, nous utilisons hello même filtre d’étendue utilisée en tant que *» dans depuis AD-utilisateur commun »* règle de synchronisation OOB, ce qui empêche la règle de synchronisation hello appliqué tooUser les objets créés par le biais d’écriture différée des utilisateurs Azure AD fonctionnalité. Vous devrez peut-être tootweak hello filtre d’étendue en fonction de tooyour déploiement d’Azure AD Connect.

6. Accédez toohello **onglet Transformation** et implémenter hello règle de transformation :
 
    | Type de flux | Attribut cible | Source | Appliquer une seule fois | Type de fusion |
    | --- | --- | --- | --- | --- |
    | Directement | PreferredDataLocation | Sélectionnez l’attribut source de hello | Désactivé | Mettre à jour |

7. Cliquez sur **ajouter** règle de trafic entrant toocreate hello.

![Créer une règle de synchronisation de trafic entrant](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>Étape 5 : Créer un attribut valeur tooAzure AD synchronisation sortante règle tooflow hello
règle de synchronisation sortante Hello permet tooflow de valeur d’attribut hello à partir de l’attribut de PreferredDataLocation toohello hello du métaverse dans Azure AD :

1. Accédez toohello **les règles de synchronisation** éditeur.

2. Définir un filtre de recherche hello **Direction** toobe **sortant**.

3. Cliquez sur le bouton **Ajouter une nouvelle règle**.

4. Sous hello **Description** , onglet de fournir hello configuration suivante :

    | Attribut | Valeur | Détails |
    | --- | --- | --- |
    | Nom | *Donnez-lui un nom* | Par exemple, « sortie tooAAD – utilisateur PreferredDataLocation » |
    | Description | *Fournissez une description* |
    | Système connecté | *Sélectionnez le connecteur de hello AAD* |
    | Type d’objet système connecté | Utilisateur ||
    | Type d’objet métaverse | **Person** ||
    | Type de lien | **Join** ||
    | Precedence | *Choisissez une valeur comprise entre 1 et 99* | Les valeurs de 1 à 99 sont réservées aux règles de synchronisation personnalisées. YDo ne récupère pas de valeur utilisée par une autre règle de synchronisation. |

5. Accédez toohello **Scoping filter** onglet et ajouter un **groupe de filtre d’étendue unique avec deux clauses**:
 
    | Attribut | Opérateur  | Valeur |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Utilisateur |
    | cloudMastered | NOTEQUAL | true |

    Le filtre d’étendue détermine les objets Active Directory auxquels cette règle de synchronisation de trafic sortant s’applique. Dans cet exemple, nous utilisons hello même filtre d’étendue à partir de « Out tooAD : identité de l’utilisateur » règle de synchronisation OOB. Il empêche règle de synchronisation hello de tooUser appliqué les objets qui ne sont pas synchronisés à partir d’Active Directory local. Vous devrez peut-être tootweak hello filtre d’étendue en fonction de tooyour déploiement d’Azure AD Connect.
    
6. Accédez toohello **Transformation** onglet et implémenter hello règle de transformation :

    | Type de flux | Attribut cible | Source | Appliquer une seule fois | Type de fusion |
    | --- | --- | --- | --- | --- |
    | Directement | PreferredDataLocation | PreferredDataLocation | Désactivé | Mettre à jour |

7. Fermer **ajouter** règle de trafic sortant toocreate hello.

![Créer une règle de synchronisation de trafic sortant](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>Étape 6 : exécuter un cycle de synchronisation complète
En règle générale, le cycle de synchronisation complète est requis, car nous avons ajouté hello de tooboth nouveaux attributs Active Directory et schéma du connecteur Azure AD et a introduit des règles de synchronisation personnalisées. Il est recommandé de vérifier les modifications hello avant de les exporter tooAzure AD. Vous pouvez utiliser hello suite des modifications de hello étapes tooverify lors de l’exécution manuellement les étapes hello qui composent un cycle de synchronisation. 

1. Exécutez **importation intégrale** étape sur hello **le connecteur Active Directory local**:

   1. Accédez toohello **Operations** onglet Bonjour Synchronization Service Manager.

   2. Avec le bouton droit sur hello **le connecteur Active Directory local** et sélectionnez **exécuter...**

   3. Dans la boîte de dialogue contextuelle hello, sélectionnez **importation intégrale** et cliquez sur **OK**.
    
   4. Attendez que toocomplete de l’opération.

    > [!NOTE]
    > Vous pouvez ignorer l’importation intégrale sur hello AD connecteur local si l’attribut source de hello est déjà inclus dans la liste hello d’attributs importés. En d’autres termes, vous n’avez pas toomake toute modification pendant [étape 2 : ajouter hello source attribut toohello AD connecteur local schéma](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).

2. Exécutez **importation intégrale** étape sur hello **connecteur Azure AD**:

   1. Avec le bouton droit sur hello **connecteur Azure AD** et sélectionnez **exécuter...**

   2. Dans la boîte de dialogue contextuelle hello, sélectionnez **importation intégrale** et cliquez sur **OK**.
   
   3. Attendez que toocomplete de l’opération.

3. Vérifier les modifications de règle de synchronisation hello sur un objet utilisateur existant :

attribut de source de Hello sur site Active Directory et PreferredDataLocation d’Azure AD ont été importés dans hello respectifs d’espace connecteur. Avant de procéder à l’étape de synchronisation complète, il est recommandé d’effectuer une **aperçu** sur un utilisateur existant objet Bonjour local espace de connecteur Active Directory. objet Hello que vous avez choisis doit avoir l’attribut source hello. Réussite **aperçu** hello PreferredDataLocation remplie Bonjour métaverse est un bon indicateur que vous avez correctement configuré les règles de synchronisation hello. Pour plus d’informations sur la façon toodo un **aperçu**, consultez toosection [vérifier hello modification](#verify-the-change).

4. Exécutez **synchronisation complète** étape sur hello **le connecteur Active Directory local**:

   1. Avec le bouton droit sur hello **le connecteur Active Directory local** et sélectionnez **exécuter...**
  
   2. Dans la boîte de dialogue contextuelle hello, sélectionnez **synchronisation complète** et cliquez sur **OK**.
   
   3. Attendez que toocomplete de l’opération.

5. Vérifiez **exportations en attente** tooAzure AD :

   1. Avec le bouton droit sur hello **connecteur Azure AD** et sélectionnez **espace de connecteur de recherche**.

   2. Dans la boîte de dialogue contextuelle hello espace de connecteur de recherche :

      1. Définissez **étendue** trop**exporter en attente**.
      
      2. Activez les trois cases à cocher : **Ajouter, Modifier et Supprimer**.
      
      3. Cliquez sur hello **recherche** liste hello tooget d’objets avec toobe modifications exporté. modifications de hello tooexamine pour un objet donné, double-cliquez sur l’objet de hello.
      
      4. Vérifiez que les modifications de hello sont prévues.

6. Exécutez **exporter** étape sur hello **connecteur Azure AD**
      
   1. Avec le bouton hello **connecteur Azure AD** et sélectionnez **exécuter...**
   
   2. Dans la boîte de dialogue contextuelle hello exécuter le connecteur, sélectionnez **exporter** et cliquez sur **OK**.
   
   3. Attendez l’exportation tooAzure AD toocomplete.

> [!NOTE]
> Vous pouvez remarquer que les étapes de hello n’incluent pas les étapes de synchronisation complète hello et exportation sur hello connecteur Azure AD. procédure de Hello n’est pas obligatoire, car les valeurs d’attribut hello passent de locale Active Directory tooAzure AD uniquement.

### <a name="step-7-re-enable-sync-scheduler"></a>Étape 7 : réactiver le planificateur de synchronisation
Réactiver le Planificateur de synchronisation intégré hello :

1. Lancez une session PowerShell.

2. Réactivez la synchronisation planifiée en exécutant l’applet de commande : `Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le modèle de configuration hello dans [approvisionnement déclaratif compréhension](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* En savoir plus sur le langage d’expression hello [compréhension des Expressions de l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).

**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
