---
title: "Didacticiel : Configuration de Workday pour l’approvisionnement automatique de l’utilisateur avec Active Directory et Azure Active Directory local | Microsoft Docs"
description: "Découvrez comment toouse Workday en tant que source de données d’identité pour Active Directory et Azure Active Directory."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>Didacticiel : Configuration de Workday pour l’approvisionnement automatique de l’utilisateur avec Active Directory et Azure Active Directory local
objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform tooimport personnes non autorisées de Workday dans Active Directory et Azure Active Directory, avec facultatif d’écriture différée de certains tooWorkday d’attributs. 



## <a name="overview"></a>Vue d'ensemble

Hello [service de configuration de l’utilisateur Azure Active Directory](active-directory-saas-app-provisioning.md) s’intègre à hello [API de ressources humaines Workday](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) commander tooprovision des comptes d’utilisateur. Azure AD utilise cette hello tooenable de connexion suivant du flux de travail de configuration utilisateur :

* **Approvisionnement d’utilisateurs tooActive active** -synchroniser des ensembles de sélectionné d’utilisateurs à partir de Workday dans une ou plusieurs forêts Active Directory. 

* **Approvisionnement d’utilisateurs uniquement dans le cloud tooAzure Active Directory** -utilisateurs de hybride qui existent dans Active Directory et Azure Active Directory peuvent être configurées en utilisant ce dernier hello [AAD Connect](connect/active-directory-aadconnect.md). Toutefois, les utilisateurs qui sont uniquement dans le cloud peuvent être configurées directement à partir de la journée de travail à l’aide de Active Directory tooAzure hello service de configuration de l’utilisateur Azure AD.

* **L’écriture différée de courrier électronique adresses tooWorkday** -service de configuration de l’utilisateur hello Azure AD peut écrire sélectionné AD Azure utilisateur attributs arrière tooWorkday, comme l’adresse de messagerie hello.

### <a name="scenarios-covered"></a>Scénarios couverts

Hello Workday l’approvisionnement d’utilisateurs pris en charge par l’utilisateur d’Azure AD hello mise en service du service de flux de travail autorise l’automatisation de hello suivant des scénarios de gestion du cycle de vie des ressources humaines et d’identité :

* **Nouvelles embauches** - lorsqu’un nouvel employé est ajouté tooWorkday, un compte d’utilisateur sera automatiquement créé dans Active Directory, Azure Active Directory et, éventuellement, Office 365 et [autres applications SaaS pris en charge par Azure AD ](active-directory-saas-app-provisioning.md), avec l’écriture arrière tooWorkday d’adresse de messagerie hello.

* **Mises à jour du profil et des attributs de l’employé** : lorsqu’un enregistrement d’employé est mis à jour dans Workday (par exemple, le nom, le titre ou le responsable), son compte d’utilisateur est automatiquement mis à jour dans Active Directory, Azure Active Directory et, éventuellement, Office 365 et [d’autres applications SaaS prises en charge par Azure AD](active-directory-saas-app-provisioning.md).

* **Résiliations de contrats d’employé** : lorsque le contrat d’un employé est résilié dans Workday, le compte d’utilisateur est automatiquement désactivé dans Active Directory, Azure Active Directory et, éventuellement, Office 365 et [d’autres applications SaaS prises en charge par Azure AD](active-directory-saas-app-provisioning.md).

* **Employé hires nouveau** : quand un employé est reloué dans Workday, son ancien compte peut être réactivé automatiquement ou tooActive redéployée (selon votre préférence) active, Azure Active Directory et éventuellement Office 365 et [autres applications SaaS pris en charge par Azure AD](active-directory-saas-app-provisioning.md).


## <a name="planning-your-solution"></a>Planification de votre solution

Avant de commencer l’intégration de votre journée de travail, vérifiez hello conditions requises ci-dessous et lecture hello suivants des conseils sur la façon de toomatch l’architecture Active Directory et les exigences de configuration de l’utilisateur hello solutions fournies par Azure Active Répertoire.

### <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure AD Premium P1 valide avec un accès administrateur général
* Un client de mise en œuvre de Workday à des fins de test et d’intégration
* Autorisations d’administrateur dans Workday toocreate un utilisateur de l’intégration système et vérifiez modifie les données employé tootest à des fins de test
* Pour tooActive répertoire de configuration de l’utilisateur, un serveur appartenant à un domaine exécutant le Service Windows 2012 ou supérieur est requis toohost hello [agent de synchronisation local](https://go.microsoft.com/fwlink/?linkid=847801)
* [Azure AD Connect](connect/active-directory-aadconnect.md) pour la synchronisation entre Active Directory et Azure AD

> [!NOTE]
> Si votre client Azure AD se trouve en Europe, consultez hello [problèmes connus](#known-issues) section ci-dessous.


### <a name="solution-architecture"></a>Architecture de solution

Azure AD fournit un riche ensemble de l’approvisionnement toohelp connecteurs que résoudre de gestion du cycle de vie de configuration et des identités à partir de Workday tooActive active, Azure AD, les applications SaaS et au-delà. Les fonctionnalités que vous allez utiliser et la manière de configurer les solutions hello varie selon l’environnement et les exigences de votre organisation. Dans un premier temps, faire l’inventaire de combien de suivant de hello sont présents et déployés dans votre organisation :

* Combien de forêts Active Directory sont en cours d’utilisation ?
* Combien de domaines Active Directory sont en cours d’utilisation ?
* Combien d’unités d’organisation (UO) Active Directory sont en cours d’utilisation ?
* Combien de clients Azure Active Directory sont en cours d’utilisation ?
* Existe-t-il des utilisateurs qui ont besoin de tooboth de toobe configuré Active Directory et Azure Active Directory (par exemple, les utilisateurs « hybride ») ?
* Existe-t-il des utilisateurs qui ont besoin de tooAzure de toobe configuré Active Directory, mais non dans Active Directory (par exemple, les utilisateurs de « cloud uniquement ») ?
* Adresses de messagerie utilisateur doivent-elles toobe tooWorkday mis à jour ?

Une fois que vous avez des questions de toothese de réponses, vous pouvez planifier votre journée de travail configuration de déploiement par guide hello suivant ci-dessous.

#### <a name="using-provisioning-connector-apps"></a>Utilisation des applications du connecteur d’approvisionnement

Azure Active Directory prend en charge des connecteurs d’approvisionnement pré-intégrés pour Workday et un grand nombre d’autres applications SaaS. 

Un seul connecteur configuration interagissant avec hello API d’un système source unique et vous aide à configurer données tooa cible unique système. La plupart des connecteurs configuration Azure AD prend en charge sont d’une source unique et d’un système de la cible (par exemple, Azure AD tooServiceNow) et peuvent être configurés en ajoutant simplement application hello en question à partir de la galerie d’applications Azure AD hello (par exemple, ServiceNow). 

Il existe une relation individuelle entre des instances de connecteurs d’approvisionnement et les instances de l’application dans Azure AD :

| Système source | Système cible |
| ---------- | ---------- | 
| Client Azure AD | Application SaaS |


Toutefois, lorsque vous travaillez avec Active Directory et de la journée de travail, il existe plusieurs toobe systèmes source et cible pris en compte :

| Système source | Système cible | Remarques |
| ---------- | ---------- | ---------- |
| Workday | Forêt Active Directory | Chaque forêt est traitée comme un système cible distinct |
| Workday | Client Azure AD | Selon les besoins pour les utilisateurs « cloud only » |
| Forêt Active Directory | Client Azure AD | Ce flux est maintenant géré par AAD Connect |
| Client Azure AD | Workday | Pour l’écriture différée des adresses e-mail |

toofacilitate ces plusieurs flux de travail toomultiple systèmes source et cible, Azure AD fournit plusieurs applications de connecteur de configuration que vous pouvez ajouter à partir de la galerie d’applications hello Azure AD :

![Galerie d’applications AAD](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **TooActive WORKDAY approvisionnement de l’annuaire** -cette application facilite l’approvisionnement de comptes utilisateur à partir de Workday tooa forêt Active Directory. Si vous avez plusieurs forêts, vous pouvez ajouter une instance de cette application à partir de la galerie d’applications Azure AD hello pour chaque forêt Active Directory que vous avez besoin de tooprovision pour.

* **TooAzure WORKDAY AD Provisioning** -tandis que AAD Connect est l’outil hello qui doit être utilisés toosynchronize Active Directory utilisateurs tooAzure Active Directory, cette application peut être utilisé toofacilitate approvisionnement d’utilisateurs uniquement dans le cloud à partir de tooa Workday unique Client de Azure Active Directory.

* **L’écriture différée WORKDAY** -facilite l’écriture différée des adresses de messagerie de l’utilisateur à partir d’Azure Active Directory tooWorkday cette application.

> [!TIP]
> Hello régulière « Journée de travail » application est utilisée pour configurer l’authentification unique entre la journée de travail et Azure Active Directory. 

Comment tooset installer et configurer ces spéciaux approvisionnement des applications de connecteur est sujet hello Hello restant des sections de ce didacticiel. Les applications que vous choisissez tooconfigure dépendront de systèmes sur lesquels vous devez tooprovision et le nombre de forêts Active Directory et Azure AD les clients sont dans votre environnement.

![Vue d'ensemble](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Configurer un utilisateur de l’intégration système dans Workday
Il est généralement nécessaire de tous les connecteurs de provisionnement Workday hello qu'ils nécessitent des informations d’identification pour un toohello tooconnect de compte dans Workday système intégration Workday ressources humaines API. Cette section décrit comment toocreate un intégrateur de système de compte dans la journée de travail.

> [!NOTE]
> Il est possible de toobypass cette procédure et à la place utiliser un compte d’administrateur général Workday en tant que compte de système d’intégration hello. Cette procédure, bien qu’adaptée aux démonstrations, n’est pas recommandée pour les déploiements de production.

### <a name="create-an-integration-system-user"></a>Créer un utilisateur de système d’intégration

**toocreate un utilisateur système d’intégration :**

1. Connectez-vous à votre client Workday à l’aide d’un compte d’administrateur. Bonjour **banc d’essai Workday**, entrez créer un utilisateur dans la zone de recherche hello, puis cliquez sur **créer utilisateur système d’intégration**. 
   
    ![Créer un utilisateur](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Créer un utilisateur")
2. Hello complète **créer utilisateur système d’intégration** tâche, vous devez fournir un nom d’utilisateur et un mot de passe pour un nouvel utilisateur de système d’intégration.  
 * Laissez hello **nécessitent de nouveau mot de passe à la prochaine connexion de** option est désactivée, car cet utilisateur sera connecté par programmation. 
 * Laissez hello **Minutes de délai d’expiration de Session** avec sa valeur par défaut de 0, ce qui empêchera hello sessions utilisateur d’expirer prématurément. 
   
    ![Créer un utilisateur de système d’intégration](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Créer un utilisateur de système d’intégration")

### <a name="create-a-security-group"></a>Créer un groupe de sécurité
Vous devez toocreate un groupe de sécurité d’intégration sans contraintes système et que vous affectez hello utilisateur tooit.

**toocreate un groupe de sécurité :**

1. Entrez créer un groupe de sécurité dans la zone de recherche hello, puis cliquez sur **créer un groupe de sécurité**. 
   
    ![Créer un groupe de sécurité](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "Créer un groupe de sécurité")
2. Hello complète **créer un groupe de sécurité** tâche.  
3. Sélectionnez le groupe de sécurité intégration système, sans contrainte de hello **Type de groupe de sécurité avec clients** liste déroulante.
4. Créer un toowhich du groupe de sécurité membres seront explicitement ajoutés. 
   
    ![Créer un groupe de sécurité](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "Créer un groupe de sécurité")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Affecter le groupe de sécurité du système utilisateur toohello hello intégration

**utilisateur système d’intégration tooassign hello :**

1. Entrez modifier le groupe de sécurité dans la zone de recherche hello, puis cliquez sur **modifier le groupe de sécurité**. 
   
    ![Modifier un groupe de sécurité](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Modifier un groupe de sécurité")
2. Recherchez et sélectionnez le nouveau groupe de sécurité d’intégration hello par nom. 
   
    ![Modifier un groupe de sécurité](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Modifier un groupe de sécurité")
3. Ajoutez hello nouvelle intégration système utilisateur toohello nouveau groupe de sécurité. 
   
    ![Groupe de sécurité système](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "Groupe de sécurité système")  

### <a name="configure-security-group-options"></a>Configurer les options du groupe de sécurité
Dans cette étape, vous accordez toohello de sécurité des autorisations de groupe pour **obtenir** et **Put** opérations sur les objets hello sécurisés par hello suivant des stratégies de sécurité de domaine :

* External Account Provisioning
* Worker Data: Public Worker Reports
* Worker Data: All Positions
* Worker Data: Current Staffing Information
* Worker Data: Business Title on Worker Profile

**options de groupe de sécurité tooconfigure :**

1. Entrez les stratégies de sécurité de domaine dans la zone de recherche hello, puis cliquez sur le lien de hello **des stratégies de sécurité de domaine pour la zone fonctionnelle**.  
   
    ![Stratégies de sécurité de domaine](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Stratégies de sécurité de domaine")  
2. Recherchez système et sélectionnez hello **système** zone fonctionnelle.  Cliquez sur **OK**.  
   
    ![Stratégies de sécurité de domaine](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Stratégies de sécurité de domaine")  
3. Dans la liste de hello des stratégies de sécurité pour la zone fonctionnelle de système de hello, développez **Administration de la sécurité** et sélectionnez la stratégie de sécurité de domaine hello **approvisionnement de compte externe**.  
   
    ![Stratégies de sécurité de domaine](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Stratégies de sécurité de domaine")  
4. Cliquez sur **modifier les autorisations**, puis, sous hello **modifier les autorisations**boîte de dialogue, ajoutez hello nouvelle sécurité groupe toohello liste des groupes de sécurité avec **obtenir** et **Put** autorisations d’intégration. 
   
    ![Modifier l’autorisation](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Modifier l’autorisation")  
5. Répétez l’étape 1 ci-dessus écran de toohello tooreturn pour la sélection des zones fonctionnelles, et cette fois, recherchez personnel, sélectionnez hello **personnel zone fonctionnelle** et cliquez sur **OK**.
   
    ![Stratégies de sécurité de domaine](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Stratégies de sécurité de domaine")  
6. Dans la liste de hello des stratégies de sécurité pour hello domaine fonctionnel personnel, développez **données des collaborateurs : personnel** et répétez l’étape 4 ci-dessus pour chacune de ces stratégies de sécurité restantes :

   * Worker Data: Public Worker Reports
   * Worker Data: All Positions
   * Worker Data: Current Staffing Information
   * Worker Data: Business Title on Worker Profile
   
7. Répétez l’étape 1 ci-dessus, l’écran de toohello tooreturn pour la sélection des zones fonctionnelles et cette fois, recherchent **les informations de Contact**, sélectionnez le domaine fonctionnel personnel de hello, puis cliquez sur **OK**.

8.  Dans la liste de hello des stratégies de sécurité pour hello domaine fonctionnel personnel, développez **les données de travail : informations de Contact de travail**et répétez l’étape 4 ci-dessus pour les stratégies de sécurité hello ci-dessous :

    * Informations sur l’employé : Adresse e-mail professionnelle

    ![Stratégies de sécurité de domaine](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Stratégies de sécurité de domaine")  
    
### <a name="activate-security-policy-changes"></a>Activer les modifications de la stratégie de sécurité

**modifications de stratégie de sécurité tooactivate :**

1. Entrez activer dans la zone de recherche hello, puis cliquez sur le lien de hello **activer les modifications de stratégie de sécurité en attente**. 
   
    ![Activer](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activer") 
2. BEGIN hello activer les modifications de stratégie de sécurité en attente de tâches en entrant un commentaire à des fins d’audit, puis cliquez sur **OK**. 
   
    ![Activer la sécurité en attente](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activer la sécurité en attente")   
3. Tâche terminée hello sur l’écran suivant de hello en activant la case à cocher hello **confirmer**, puis cliquez sur **OK**. 
   
    ![Activer la sécurité en attente](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activer la sécurité en attente")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Configuration des utilisateurs à partir de Workday tooActive Active
Suivez ces instructions tooconfigure utilisateur de configuration de compte à partir de Workday tooeach forêt Active Directory dont vous avez besoin pour l’approvisionnement.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Partie 1 : Ajout d’application de connecteur configuration hello et la création d’hello connexion tooWorkday

**tooconfigure Workday tooActive approvisionnement de l’annuaire :**

1.  Accédez trop<https://portal.azure.com>

2.  Dans la barre de navigation gauche hello, sélectionnez **Azure Active Directory**

3.  Cliquez sur **Applications d’entreprise**, puis sur **Toutes les applications**.

4.  Sélectionnez **ajouter une application**et sélectionnez hello **tous les** catégorie.

5.  Recherchez **tooActive Workday configuration active**, puis ajoutez cette application à partir de la galerie de hello.

6.  Après avoir hello l’application est ajoutée et écran de détails de l’application hello est affichée, sélectionnez **Provisioning**

7.  Hello de modification **Provisioning** **Mode** trop**automatique**

8.  Hello complète **informations d’identification administrateur** section comme suit :

   * **Admin Username** – entrer de nom d’utilisateur de hello Hello compte de système d’intégration Workday, ajouté un nom de domaine du locataire hello. **Le résultat doit être le suivant : username@contoso4**

   * **Mot de passe administrateur –** Hello compte de système d’intégration Workday, entrez le mot hello

   * **URL de locataire** entrez hello toohello Workday web services point de terminaison URL pour votre client. Cela doit ressembler à : https://wd3-impl-services1.workday.com/ccx/service/contoso4, où contoso4 est remplacé par le nom de votre locataire approprié et wd3-impl est remplacé par la chaîne hello correct.

   * **Forêt Active Directory -** hello « Name » de votre forêt Active Directory, tel que retourné par l’applet de commande powershell Get-ADForest de hello. Il s’agit généralement d’une chaîne telle que : *contoso.com*

   * **Conteneur d’Active Directory -** Entrez une chaîne hello conteneur qui contient tous les utilisateurs de votre forêt Active Directory. Exemple : *OU = Utilisateurs standard, OU = Utilisateurs, DC = contoso, DC = test*

   * **E-mail de notification :** entrez votre adresse e-mail et cochez la case « Envoyer par e-mail en cas de défaillance ».

   * Cliquez sur hello **tester la connexion** bouton. Si un test de connexion hello réussit, cliquez sur hello **enregistrer** bouton en haut de hello. En cas d’échec, vérifiez que les informations d’identification de la journée de travail hello sont valides dans la journée de travail. 

![Portail Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>Partie 2 : configuration des mappages d’attributs 

Dans cette section, vous allez configurer le flux des données de l’utilisateur de Workday vers Active Directory.

1.  Sur l’onglet d’approvisionnement hello sous **mappages**, cliquez sur **tooOnPremises de synchroniser les employés de Workday**.

2.  Bonjour **portée d’objet Source** champ, vous pouvez sélectionner les ensembles d’utilisateurs dans la journée de travail doivent être dans la portée pour la configuration tooAD, en définissant un ensemble de filtres basés sur l’attribut. étendue de Hello par défaut est « tous les utilisateurs dans la journée de travail ». Exemples de filtres :

   * Exemple : Scope toousers avec l’ID de travail entre 1000000 et 2000000

      * Attribut : WorkerID

      * Opérateur : correspondance REGEX

      * Valeur : (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Exemple : uniquement les employés et non les employés du contingent 

      * Attribut : EmployeeID

      * Opérateur : n’est pas NULL

3.  Bonjour **Actions de l’objet cible** champ, vous pouvez filtrer globalement les actions autorisées toobe effectuée dans Active Directory. Les actions **Créer** et **Mettre à jour** sont les plus courantes.

4.  Bonjour **mappages d’attributs** section, vous pouvez définir chaque journée de travail attributs mappent les attributs d’annuaire tooActive.

5. Cliquez sur un tooupdate de mappage attribut existant, ou cliquez sur **Ajouter nouveau mappage** bas hello de nouveaux mappages hello écran tooadd. Un mappage d’attribut individuel prend en charge les propriétés suivantes :

      * **Type de mappage**

         * **Direct** – écrit la valeur hello hello Workday toohello AD attribut, sans aucune modification

         * **Constante** -écrire une valeur de chaîne constante statique pour l’attribut de hello AD

         * **Expression** – vous permet de toowrite une valeur personnalisée à l’attribut hello AD, basé sur un ou plusieurs attributs de la journée de travail. [Pour plus d’informations, consultez l’article sur les expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **Attribut source** -attribut utilisateur hello journée de travail.

      * **Valeur par défaut** : facultatif. Si l’attribut de source de hello possède une valeur vide, mappage de hello écrire cette valeur.
            Configuration la plus courante est tooleave ce vide.

      * **Attribut cible** : attribut d’utilisateur hello dans Active Directory.

      * **Correspond à des objets à l’aide de cet attribut** : ce mappage doit être utilisé ou non toouniquely identifier les utilisateurs entre Active Directory et de la journée de travail. Cela est généralement définie dans le champ ID de travail pour la journée de travail, qui est généralement mappée à un des attributs d’ID d’employé hello dans Active Directory.

      * **Priorité des correspondances** : plusieurs attributs de correspondance peuvent être définis. S’il en existe plusieurs, ils sont évalués dans l’ordre défini par ce champ. Dès qu’une correspondance est trouvée, aucun autre attribut correspondant n’est évalué.

      * **Appliquer ce mappage**
       
         * **Toujours** : appliquez ce mappage à la création de l’utilisateur et aux actions de mise à jour

         * **Lors de la création uniquement** : appliquez ce mappage uniquement aux actions de création utilisateur

6. Cliquez sur les mappages de votre toosave **enregistrer** haut hello de la section de mappage d’attribut.

![Portail Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**Vous trouverez ci-dessous quelques exemples de mappages d’attributs entre Workday et Active Directory, avec certaines expressions communes**

-   expression Hello qui mappe toohello parentDistinguishedName AD attribut peut être utilisée tooprovision un tooa utilisateur unité d’organisation spécifique basée sur un ou plusieurs attributs de source de Workday. Cet exemple place les utilisateurs dans différentes unités d’organisation en fonction des données de ville dans Workday.

-   expression Hello qui mappe l’attribut userPrincipalName AD de toohello créer un UPN de firstName.LastName@contoso.com. Elle remplace également des caractères spéciaux non conformes.

-   [Il existe une documentation sur l’écriture d’expressions ici](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| ATTRIBUT WORKDAY | ATTRIBUT ACTIVE DIRECTORY |  CORRESPONDANCE D’ID ? | CRÉER / METTRE À JOUR |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  EmployeeID | **Oui** | Écrit lors de la création uniquement | 
|  **Municipalité**   |   l   |     | Créer + mettre à jour |
|  **Société**         | société   |     |  Créer + mettre à jour |
|  **CountryReferenceTwoLetter**      |   co |     |   Créer + mettre à jour |
| **CountryReferenceTwoLetter**    |  c  |     |         Créer + mettre à jour |
| **SupervisoryOrganization**  | department  |     |  Créer + mettre à jour |
|  **PreferredNameData**  |  displayName |     |   Créer + mettre à jour |
| **EmployeeID**    |  cn    |   |   Écrit lors de la création uniquement |
| **Fax**      | facsimileTelephoneNumber     |     |    Créer + mettre à jour |
| **FirstName**   | givenName       |     |    Créer + mettre à jour |
| **Commuter (\[Active\], « 0 », « True », « 1 »,)** |  accountDisabled      |     | Créer + mettre à jour |
| **Mobile**  |    mobile       |     |       Écrit lors de la création uniquement |
| **EmailAddress**    | mail    |     |     Créer + mettre à jour |
| **ManagerReference**   | manager  |     |  Créer + mettre à jour |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  Créer + mettre à jour |
| **PostalCode**  |   postalCode  |     | Créer + mettre à jour |
| **LocalReference** |  preferredLanguage  |     |  Créer + mettre à jour |
| **Remplacer(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.) \*\$](file:///\\.) *$)", , "", , )**      |    sAMAccountName            |     |         Écrit lors de la création uniquement |
| **LastName**   |   sn   |     |  Créer + mettre à jour |
| **CountryRegionReference** |  st     |     | Créer + mettre à jour |
| **AddressLineData**    |  streetAddress  |     |   Créer + mettre à jour |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | Écrit lors de la création uniquement |
| **BusinessTitle**   |  title     |     |  Créer + mettre à jour |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**   | userPrincipalName     |     | Créer + mettre à jour                                                   
| **Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**  | parentDistinguishedName     |     |  Créer + mettre à jour |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>Partie 3 : Configurer l’agent de synchronisation local hello

Dans l’ordre tooActive de tooprovision répertoire local, un agent doit être installé sur un serveur appartenant à un domaine dans le désir hello forêt Active Directory. Informations d’identification sont requises pour terminer la procédure de hello administrateur de domaine (ou administrateur d’entreprise).

**[Vous pouvez télécharger hello localement l’agent de synchronisation ici](https://go.microsoft.com/fwlink/?linkid=847801)**

Après l’installation de l’agent, exécutez les commandes de Powershell de hello sous l’agent de hello tooconfigure pour votre environnement.

**Commande #1**

> cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent

> import-module AADSyncAgent.psd1

**Commande #2**

> Add-ADSyncAgentActiveDirectoryConfiguration

* Entrée : « Comme nom de répertoire », entrez nom hello Active Directory de la forêt, tel qu’il est entré dans la partie \#2
* Entrée : nom d’utilisateur administrateur et mot de passe pour la forêt Active Directory

**Commande #3**

> Add-ADSyncAgentAzureActiveDirectoryConfiguration

* Entrée : nom d’utilisateur administrateur global et mot de passe pour votre client Azure AD

**Commande #4**

> Get-AdSyncAgentProvisioningTasks

* Action : Vérifiez que les données sont retournées. Cette commande détecte automatiquement les applications d’approvisionnement Workday dans votre client Azure AD. Exemple de sortie :

> Nom : Ma forêt AD
>
> Activé : True
>
> Nom du répertoire : mydomain.contoso.com
>
> Basées sur les références : False
>
> Identificateur : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**Commande #5**

> Start-AdSyncAgentSynchronization -Automatic

**Commande #6**

> net stop aadsyncagent

**Commande #7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>Partie 4 : Démarrer le service hello
Une fois que les parties 1 à 3 ont été effectuées, vous pouvez démarrer hello service dans hello portail de gestion de configuration.

1.  Bonjour **Provisioning** ensemble hello, onglet **état d’approvisionnement** à **sur**.

2. Cliquez sur **Enregistrer**.

3. Ceci démarrera la synchronisation initiale hello, qui peut prendre un nombre variable d’heures en fonction du nombre d’utilisateurs dans la journée de travail.

4. Événements de synchronisation individuels tels que les utilisateurs sont lus en dehors de la journée de travail, et puis tooActive par la suite ajoutée ou mises à jour active, peuvent être consultées dans hello **les journaux d’Audit** onglet. **[Consultez hello configuration guide de création de rapports pour obtenir des instructions détaillées sur le fonctionnement des journaux d’audit de hello tooread](active-directory-saas-provisioning-reporting.md)**

5.  journal des applications Windows Hello sur l’ordinateur agent hello affiche toutes les opérations effectuées via l’agent de hello.

6. Une fois cette opération terminée, un rapport de synthèse de l’audit est écrit dans l’onglet **Approvisionnement**, comme indiqué ci-dessous.

![Portail Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>Configuration de configuration tooAzure Active Directory de l’utilisateur
La configuration de mise en service tooAzure Active Directory dépend de vos exigences de configuration, comme indiqué dans le tableau hello ci-dessous.

| Scénario | Solution |
| -------- | -------- |
| **Les utilisateurs doivent toobe configuré tooActive Directory et Azure AD** | Utilisez  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Les utilisateurs besoin toobe configuré tooActive active uniquement** | Utilisez  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Les utilisateurs doivent toobe configuré tooAzure AD uniquement (cloud uniquement)** | Hello d’utilisation **configuration d’Active Directory Workday tooAzure** application dans la galerie d’applications hello |

Pour obtenir des instructions sur la configuration d’Azure AD Connect, consultez hello [documentation d’Azure AD Connect](connect/active-directory-aadconnect.md).

Hello les sections suivantes décrire la configuration d’une connexion entre la journée de travail et Azure AD tooprovision cloud uniquement les utilisateurs.

> [!IMPORTANT]
> Uniquement procédure hello ci-dessous si vous avez uniquement dans le cloud des utilisateurs qui ont besoin toobe configuré tooAzure AD et non localement dans Active Directory.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Partie 1 : Ajout d’application de connecteur configuration hello Azure AD et la création d’hello connexion tooWorkday

**tooconfigure Workday tooAzure Active Directory de configuration pour les utilisateurs de cloud uniquement :**

1.  Accédez trop<https://portal.azure.com>.

2.  Dans la barre de navigation gauche hello, sélectionnez **Azure Active Directory**

3.  Cliquez sur **Applications d’entreprise**, puis sur **Toutes les applications**.

4.  Sélectionnez **ajouter une application**, puis sélectionnez hello **tous les** catégorie.

5.  Recherchez **configuration de Workday tooAzure AD**, puis ajoutez cette application à partir de la galerie de hello.

6.  Après avoir hello l’application est ajoutée et écran de détails de l’application hello est affichée, sélectionnez **Provisioning**

7.  Hello de modification **Provisioning** **Mode** trop**automatique**

8.  Hello complète **informations d’identification administrateur** section comme suit :

   * **Admin Username** – entrer de nom d’utilisateur de hello Hello compte de système d’intégration Workday, ajouté un nom de domaine du locataire hello. Le résultat doit être le suivant : username@contoso4

   * **Mot de passe administrateur –** Hello compte de système d’intégration Workday, entrez le mot hello

   * **URL de locataire** entrez hello toohello Workday web services point de terminaison URL pour votre client. Cela doit ressembler à : https://wd3-impl-services1.workday.com/ccx/service/contoso4, où contoso4 est remplacé par le nom de votre locataire approprié et wd3-impl est remplacé par la chaîne hello approprié (si nécessaire).

   * **E-mail de notification :** entrez votre adresse e-mail et cochez la case « Envoyer par e-mail en cas de défaillance ».

   * Cliquez sur hello **tester la connexion** bouton.

   * Si un test de connexion hello réussit, cliquez sur hello **enregistrer** bouton en haut de hello. En cas d’échec, vérifiez que l’URL de Workday hello et informations d’identification sont valides dans la journée de travail.


### <a name="part-2-configure-attribute-mappings"></a>Partie 2 : configuration des mappages d’attributs 

Dans cette section, vous allez configurer le flux des données de Workday vers Azure Active Directory pour l’utilisateur « cloud only ».

1.  Sur l’onglet d’approvisionnement hello sous **mappages**, cliquez sur **tooAzure de synchroniser les threads de travail AD**.

2.   Bonjour **portée d’objet Source** champ, vous pouvez sélectionner les ensembles d’utilisateurs dans la journée de travail doivent être dans la portée pour la configuration tooAzure AD, en définissant un ensemble de filtres basés sur l’attribut. étendue de Hello par défaut est « tous les utilisateurs dans la journée de travail ». Exemples de filtres :

   * Exemple : Scope toousers avec l’ID de travail entre 1000000 et 2000000

      * Attribut : WorkerID

      * Opérateur : correspondance REGEX

      * Valeur : (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Exemple : uniquement les employés du contingent et pas les employés réguliers

      * Attribut : ContingentID

      * Opérateur : n’est pas NULL

3.  Bonjour **Actions de l’objet cible** champ, vous pouvez filtrer globalement les actions autorisées toobe effectuée sur Azure AD. Les actions **Créer** et **Mettre à jour** sont les plus courantes.

4.  Bonjour **mappages d’attributs** section, vous pouvez définir chaque journée de travail attributs mappent les attributs d’annuaire tooActive.

5. Cliquez sur un tooupdate de mappage attribut existant, ou cliquez sur **Ajouter nouveau mappage** bas hello de nouveaux mappages hello écran tooadd. Un mappage d’attribut individuel prend en charge les propriétés suivantes :

   * **Type de mappage**

      * **Direct** – écrit la valeur hello hello Workday toohello AD attribut, sans aucune modification

      * **Constante** -écrire une valeur de chaîne constante statique pour l’attribut de hello AD

      * **Expression** – vous permet de toowrite une valeur personnalisée à l’attribut hello AD, basé sur un ou plusieurs attributs de la journée de travail. [Pour plus d’informations, consultez l’article sur les expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **Attribut source** -attribut utilisateur hello journée de travail.

   * **Valeur par défaut** : facultatif. Si l’attribut de source de hello possède une valeur vide, mappage de hello écrire cette valeur.
            Configuration la plus courante est tooleave ce vide.

   * **Attribut cible** : attribut d’utilisateur hello dans Azure AD.

   * **Correspond à des objets à l’aide de cet attribut** : ce mappage doit être utilisé ou non toouniquely identifier les utilisateurs entre la journée de travail et Azure AD. Cela est généralement définie dans le champ ID de travail pour la journée de travail, qui est généralement mappée à l’attribut d’ID d’employé hello (nouveau) ou un attribut d’extension dans Azure AD.

   * **Priorité des correspondances** : plusieurs attributs de correspondance peuvent être définis. S’il en existe plusieurs, ils sont évalués dans l’ordre défini par ce champ. Dès qu’une correspondance est trouvée, aucun autre attribut correspondant n’est évalué.

   * **Appliquer ce mappage**

     * **Toujours** : appliquez ce mappage à la création de l’utilisateur et aux actions de mise à jour

     * **Lors de la création uniquement** : appliquez ce mappage uniquement aux actions de création utilisateur

6. Cliquez sur les mappages de votre toosave **enregistrer** haut hello de la section de mappage d’attribut.

### <a name="part-3-start-hello-service"></a>Partie 3 : Démarrer le service hello
Une fois que les parties 1 et 2 ont été effectuées, vous pouvez démarrer hello service de configuration.

1.  Bonjour **Provisioning** ensemble hello, onglet **état d’approvisionnement** à **sur**.

2. Cliquez sur **Enregistrer**.

3. Ceci démarrera la synchronisation initiale hello, qui peut prendre un nombre variable d’heures en fonction du nombre d’utilisateurs dans la journée de travail.

4. Événements de synchronisation individuels peuvent être affichés dans hello **les journaux d’Audit** onglet. **[Consultez hello configuration guide de création de rapports pour obtenir des instructions détaillées sur le fonctionnement des journaux d’audit de hello tooread](active-directory-saas-provisioning-reporting.md)**

5. Une fois cette opération terminée, un rapport de synthèse de l’audit est écrit dans l’onglet **Approvisionnement**, comme indiqué ci-dessous.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>Configuration de l’écriture différée de tooWorkday des adresses de messagerie
Suivez ces instructions tooconfigure écriture différée des mots utilisateur des adresses de messagerie à partir d’Azure Active Directory tooWorkday.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Partie 1 : Ajout d’application de connecteur configuration hello et la création d’hello connexion tooWorkday

**tooconfigure Workday tooActive approvisionnement de l’annuaire :**

1.  Accédez trop<https://portal.azure.com>

2.  Dans la barre de navigation gauche hello, sélectionnez **Azure Active Directory**

3.  Cliquez sur **Applications d’entreprise**, puis sur **Toutes les applications**.

4.  Sélectionnez **ajouter une application**, puis sélectionnez hello **tous les** catégorie.

5.  Recherchez **l’écriture différée de la journée de travail**et ajoutez cette application à partir de la galerie de hello.

6.  Après avoir hello l’application est ajoutée et écran de détails de l’application hello est affichée, sélectionnez **Provisioning**

7.  Hello de modification **Provisioning** **Mode** trop**automatique**

8.  Hello complète **informations d’identification administrateur** section comme suit :

   * **Admin Username** – entrer de nom d’utilisateur de hello Hello compte de système d’intégration Workday, ajouté un nom de domaine du locataire hello. Le résultat doit être le suivant : username@contoso4

   * **Mot de passe administrateur –** Hello compte de système d’intégration Workday, entrez le mot hello

   * **URL de locataire** entrez hello toohello Workday web services point de terminaison URL pour votre client. Cela doit ressembler à : https://wd3-impl-services1.workday.com/ccx/service/contoso4, où contoso4 est remplacé par le nom de votre locataire approprié et wd3-impl est remplacé par la chaîne hello approprié (si nécessaire).

   * **E-mail de notification :** entrez votre adresse e-mail et cochez la case « Envoyer par e-mail en cas de défaillance ».

   * Cliquez sur hello **tester la connexion** bouton. Si un test de connexion hello réussit, cliquez sur hello **enregistrer** bouton en haut de hello. En cas d’échec, vérifiez que l’URL de Workday hello et informations d’identification sont valides dans la journée de travail.


### <a name="part-2-configure-attribute-mappings"></a>Partie 2 : configuration des mappages d’attributs 


Dans cette section, vous allez configurer le flux des données de l’utilisateur de Workday vers Active Directory.

1.  Sur l’onglet d’approvisionnement hello sous **mappages**, cliquez sur **aux utilisateurs de synchroniser les Azure AD tooWorkday**.

2.  Bonjour **portée d’objet Source** champ, vous pouvez éventuellement filtrer les ensembles d’utilisateurs dans Azure Active Directory ont leurs adresses de messagerie réécrites dans tooWorkday. étendue de Hello par défaut est « tous les utilisateurs dans Azure AD ». 

3.  Bonjour **mappages d’attributs** section, vous pouvez définir chaque journée de travail attributs mappent les attributs d’annuaire tooActive. Il existe un mappage pour l’adresse de messagerie hello par défaut. Toutefois, hello ID correspondant doit être mis à jour toomatch utilisateurs dans Azure AD avec leurs entrées correspondantes dans la journée de travail. Une méthode correspondante populaire est toosynchronize hello Workday employé ou employee ID tooextensionAttribute1-15 dans Azure AD et ensuite utiliser cet attribut dans les utilisateurs Azure AD toomatch que dans la journée de travail.

4.  Cliquez sur les mappages de votre toosave **enregistrer** haut hello hello section de mappage d’attribut.

### <a name="part-3-start-hello-service"></a>Partie 3 : Démarrer le service hello
Une fois que les parties 1 et 2 ont été effectuées, vous pouvez démarrer hello service de configuration.

1.  Bonjour **Provisioning** ensemble hello, onglet **état d’approvisionnement** à **sur**.

2. Cliquez sur **Enregistrer**.

3. Ceci démarrera la synchronisation initiale hello, qui peut prendre un nombre variable d’heures en fonction du nombre d’utilisateurs dans la journée de travail.

4. Événements de synchronisation individuels peuvent être affichés dans hello **les journaux d’Audit** onglet. **[Consultez hello configuration guide de création de rapports pour obtenir des instructions détaillées sur le fonctionnement des journaux d’audit de hello tooread](active-directory-saas-provisioning-reporting.md)**

5. Une fois cette opération terminée, un rapport de synthèse de l’audit est écrit dans l’onglet **Approvisionnement**, comme indiqué ci-dessous.

## <a name="known-issues"></a>Problèmes connus

* **Rapports d’audit dans les paramètres régionaux européens** - comme de version hello de cette version d’évaluation technique, il existe un problème connu avec hello [journaux d’audit](active-directory-saas-provisioning-reporting.md) pour les applications de connecteur Workday hello n’apparaissent ne pas dans hello [portail Azure](https://portal.azure.com) si le client de hello AD Azure se trouve dans un centre de données européen. Un correctif pour résoudre ce problème est à venir. Veuillez vérifier cet espace à nouveau dans hello près de futures mises à jour. 

## <a name="additional-resources"></a>Ressources supplémentaires
* [Didacticiel : configurer l’authentification unique entre Workday et Azure Active Directory](active-directory-saas-workday-tutorial.md)
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Étapes suivantes

* [Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
