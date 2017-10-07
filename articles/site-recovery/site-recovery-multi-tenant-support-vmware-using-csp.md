---
title: "prise en charge d’aaaMulti-locataire de VMware VM réplication tooAzure (programme CSP) | Documents Microsoft"
description: "Décrit comment toodeploy Azure Site Recovery dans une réplication de tooorchestrate architecture mutualisée, le basculement et la récupération de local tooAzure de machines virtuelles (VM) VMware via le programme hello CSP à l’aide de hello portail Azure"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>Prise en charge de plusieurs locataire dans Azure Site Recovery pour répliquer tooAzure d’ordinateurs virtuels VMware via le fournisseur de services cryptographiques

Azure Site Recovery prend en charge les environnements multilocataires pour les abonnements de locataire. Il prend également en charge une architecture mutualisée pour les abonnements client qui sont créés et gérés via le programme hello fournisseur de solutions Microsoft Cloud (CSP). Cet article décrit en détail conseils hello pour implémenter et gérer des scénarios de VMware à Azure architecture mutualisées. Il couvre également la création et la gestion des abonnements de locataire via CSP.

Ce guide se dessine fortement à partir de la documentation existante du hello pour la réplication tooAzure d’ordinateurs virtuels VMware. Pour plus d’informations, consultez [tooAzure de machines virtuelles VMware de répliquer avec Site Recovery](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Environnements multilocataires
Il existe trois modèles multilocataires principaux :

* **Partagé du fournisseur de Services d’hébergement (HSP)**: partenaire de hello possède l’infrastructure physique de hello et utilise des ressources partagées (vCenter centres de données, stockage physique et ainsi de suite) toohost ordinateurs virtuels de plusieurs clients sur hello même infrastructure. partenaire de Hello peut fournir la gestion de la récupération d’urgence comme un service géré, ou locataire de hello peut posséder la récupération d’urgence comme une solution libre-service.

* **Dédié qui héberge un fournisseur de Services**: partenaire de hello possède l’infrastructure physique de hello mais utilise des ressources dédiées (plusieurs vCenter, magasins de données physique et ainsi de suite) toohost VMs de chaque client sur une infrastructure distincte. partenaire de Hello peut fournir la gestion de la récupération d’urgence comme un service géré, ou locataire de hello peut le propriétaire comme une solution libre-service.

* **Managed Services Provider (MSP)**: client de hello possède infrastructure hello physique qui héberge des ordinateurs virtuels de hello et partenaire de hello fournit l’activation de la récupération d’urgence et de gestion.

## <a name="shared-hosting-multi-tenant-guidance"></a>Conseils de multilocation de l’hébergement partagé
Cette section couvre scénario d’hébergement partagé hello en détail. deux autres scénarios Hello sont des sous-ensembles de scénario d’hébergement partagé hello, et ils utilisent hello mêmes principes. Hello sont décrites en fin de hello du Guide d’hébergement partagé hello.

condition de base dans un scénario de l’architecture mutualisée Hello est tooisolate hello différents clients. Un locataire ne doit pas être d’un autre client hosted tooobserve en mesure de. Dans un environnement géré par un partenaire, cette exigence n’est pas aussi importante que dans un environnement en libre-service où elle peut être critique. Ces conseils partent du principe que l’isolation des locataires est requise.

architecture de Hello est présentée dans hello suivant schéma :

![HSP partagé avec un vCenter](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**Scénario d’hébergement partagé avec un vCenter**

Comme indiqué dans hello précédant le diagramme, chaque client possède un serveur d’administration distincts. Ce client de limites de configuration accéder aux ordinateurs virtuels de tootenant spécifique et permet l’isolation des locataires. Un scénario de réplication de machine virtuelle VMware utilise hello configuration serveur toomanage comptes toodiscover machines virtuelles et installer des agents. Nous suivons hello pour les environnements d’architecture mutualisées, avec ajout hello de limiter la découverte d’ordinateurs virtuels via le serveur vCenter mêmes principes de contrôle d’accès.

spécification d’isolation des données Hello et nécessite que toutes les informations sur l’infrastructure sensibles (telles que les informations d’identification d’accès) restent tootenants non divulgué. Pour cette raison, nous recommandons que tous les composants du serveur d’administration hello restent sous contrôle exclusif de hello du partenaire de hello. composants de serveur de gestion de Hello sont :
* Serveur de configuration (CS)
* Serveur de traitement (PS)
* Serveur cible maître (MT) 

Une montée en puissance parallèle PS est également sous contrôle de code de partenaire hello.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>Chaque CS dans un scénario d’architecture mutualisée hello utilise deux comptes

- **compte d’accès vCenter**: utiliser des machines virtuelles du locataire toodiscover ce compte. Il dispose des autorisations d’accès de vCenter affectées tooit (comme décrit dans la section suivante de hello). toohelp éviter les fuites accidentelles accès, nous recommandons que les partenaires entrer ces informations d’identification, eux-mêmes dans l’outil de configuration hello.

- **Compte d’accès de machine virtuelle**: utilisez cet agent de mobilité compte tooinstall hello sur les machines virtuelles du locataire hello via un push automatique. Il est généralement un compte de domaine qu’un client peut fournir tooa partenaire ou que vous pouvez également les partenaires hello peuvent gérer directement. Si un client ne veut pas les détails de hello tooshare avec les partenaires hello directement, il ou elle peut être autorisée informations d’identification de hello tooenter à durée limitée accéder toohello CS ou, avec l’assistance du partenaire hello, installer des agents de mobilité manuellement.

### <a name="requirements-for-a-vcenter-access-account"></a>Conditions requises pour un compte d’accès vCenter

Comme indiqué dans la précédente section de hello, vous devez configurer hello CS avec un compte qui dispose d’un tooit rôle spécial attribué. attribution de rôle Hello doit être appliqué le compte d’accès vCenter toohello pour chaque objet de vCenter et pas propagées toohello des objets enfants. Cette configuration garantit l’isolation des locataires, car accès propagation peut entraîner les objets tooother accès accidentel.

![Hello propager tooChild Objects (option)](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

alternative de Hello est le compte d’utilisateur tooassign hello et de rôle au niveau de l’objet de centre de données hello et propager toohello des objets enfants. Ensuite attribuer hello compte un *aucun accès* rôle pour chaque objet (par exemple, les machines virtuelles d’autres locataires) qui doit être inaccessible tooa des client particulier. Cette configuration est fastidieuse et expose des contrôles d’accès accidentelle, car l’accès est héritée du parent de hello est automatiquement accordée à chaque nouvel objet enfant. Par conséquent, nous vous recommandons d’utiliser première approche de hello.

procédure d’accès au compte Hello vCenter est comme suit :

1. Créer un nouveau rôle en clonant hello prédéfini *en lecture seule* rôle, puis attribuez-lui un nom pratique (par exemple, Azure_Site_Recovery, comme illustré dans cet exemple).

2. Attribuer hello suivant le rôle de toothis autorisations :

    * **Banque de données** : Allouer de l’espace, Parcourir la banque de données, Opérations de fichier de bas niveau, Supprimer le fichier, Mettre à jour les fichiers de machine virtuelle

    * **Réseau** : Attribution de réseau

    * **Ressource**: pool de tooresource affecter un ordinateur virtuel, migration de machine virtuelle hors tension, migration de machine virtuelle sous tension

    * **Tâches** : Créer une tâche, Mettre à jour une tâche

    * **Machine virtuelle** : 
        * Configuration > tout
        * Interagir > Répondre à la question, Connexion d’appareil, Configurer un support de CD, Configurer une disquette, Mettre hors tension, Mettre sous tension, Installation des outils VMware
        * Inventaire > Créer à partir d’un existant, Créer, S’inscrire, Annuler l’inscription
        * Approvisionnement > Autoriser le téléchargement de machines virtuelles, Autoriser le chargement de fichiers de machine virtuelle
        * Gestion des instantanés > Supprimer les instantanés

    ![boîte de dialogue Modifier le rôle Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. Affectez des niveaux toohello vCenter compte d’accès (utilisé dans le locataire hello CS) pour différents objets, comme suit :

>| Object | Rôle | Remarques |
>| --- | --- | --- |
>| vCenter | Lecture seule | Seuls tooallow vCenter d’accès nécessaire pour la gestion des objets différents. Vous pouvez supprimer cette autorisation si le compte de hello va jamais toobe fournies tooa locataire ou pour toutes les opérations de gestion sur hello vCenter. |
>| Centre de données | Azure_Site_Recovery |  |
>| Hôte et cluster hôte | Azure_Site_Recovery | Nouveau garantit que l’accès est au niveau de l’objet hello, afin que les hôtes accessibles uniquement avoir des machines virtuelles du locataire avant le basculement et après la restauration automatique. |
>| Banque de données et cluster de banque de données | Azure_Site_Recovery | Identique à ce qui précède. |
>| Réseau | Azure_Site_Recovery |  |
>| Serveur d’administration | Azure_Site_Recovery | Inclut les composants de tooall d’accès (CS PS et MT) si une est en dehors de l’ordinateur de hello CS. |
>| Machines virtuelles de locataire | Azure_Site_Recovery | Garantit que toutes les machines virtuelles d’un locataire particulier de nouveau locataire également obtenir cet accès, ou ils ne peuvent pas être découvert par hello portail Azure. |

accès au compte de Hello vCenter est terminée. Cette étape effectue les opérations de restauration toocomplete hello autorisations minimales exigence. Vous pouvez également utiliser ces autorisations d’accès avec vos stratégies existantes. Il suffit de modifier existant autorisations ensemble tooinclude autorisations de votre rôle de l’étape 2, détaillée précédemment.

toorestrict les opérations de récupération d’urgence jusqu'à ce que l’état de basculement hello (autrement dit, sans les fonctionnalités de la restauration automatique), suivez hello précédant la procédure, avec une exception : au lieu d’affecter hello *Azure_Site_Recovery* rôle compte d’accès vCenter toohello, affecter uniquement un *en lecture seule* toothat compte membre du rôle. Ce jeu d’autorisations permet la réplication et le basculement de la machine virtuelle, et il n’autorise pas la restauration automatique. Le reste du hello précédant le processus reste en l’état. tooensure isolation des locataires et restreindre la détection de la machine virtuelle, chaque autorisation est toujours affectée au niveau toochild d’uniquement et non propagé d’objets hello.

## <a name="other-multi-tenant-environments"></a>Autres environnements multilocataires

Hello précédant la section décrite comment tooset d’un environnement à plusieurs locataire pour une solution d’hébergement partagé. Hello autres principale existe deux solutions d’hébergement dédié et de service administré. architecture de Hello pour ces solutions est décrite dans les sections suivantes de hello.

### <a name="dedicated-hosting-solution"></a>Solution d’hébergement dédié

Comme indiqué dans hello suivant schéma, hello architecturales dans une solution d’hébergement dédiée diffère infrastructure de chaque client est configurée pour ce client uniquement. Étant donné que les clients sont isolées par vCenter distinct, fournisseur d’hébergement hello doit toujours étapes hello CSP fourni pour l’hébergement partagé mais n’a pas besoin tooworry sur l’isolation des locataires. Le CSP reste inchangé.

![architecture-hsp-partagé](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**Scénario d’hébergement dédié avec plusieurs vCenter**

### <a name="managed-service-solution"></a>Solution de service géré

Comme indiqué dans hello diagramme suivant, la différence d’architecture hello dans une solution de service administré est qu’infrastructure de chaque client est également physiquement séparé à partir de l’infrastructure d’autres clients. Ce scénario existe généralement lorsque les locataires hello détient hello infrastructure et veut une récupération d’urgence toomanage solution fournisseur. Là encore, étant donné que les clients sont physiquement isolés par différentes infrastructures, partenaire de hello doit toofollow hello CSP étapes pour l’hébergement partagé mais n’a pas besoin tooworry sur l’isolation des locataires. L’approvisionnement CSP reste inchangé.

![architecture-hsp-partagé](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**Scénario de service géré avec plusieurs vCenter**

## <a name="csp-program-overview"></a>Vue d’ensemble du programme CSP
Hello [programme du fournisseur de services cryptographiques](https://partner.microsoft.com/en-US/cloud-solution-provider) favorise favorisant la collaboration récits qui offrent aux partenaires tous les services de cloud de Microsoft, notamment Office 365, Enterprise Mobility Suite et Microsoft Azure. Avec le fournisseur de services cryptographiques, nos partenaires possèdent la relation de bout en bout hello avec les clients et convertir en point de contact principal relation hello. Partenaires déploiement abonnements Azure pour les clients et combiner des abonnements hello avec leurs propres offres personnalisées à valeur ajoutée.

Avec Azure Site Recovery, partenaires peuvent gérer des solutions de récupération d’urgence complète hello pour les clients directement via le fournisseur de services cryptographiques. Ou ils peuvent utiliser tooset CSP des environnements de récupération de Site et permettre aux clients de gérer leurs propres besoins de récupération d’urgence d’une manière libre service. Dans les deux cas, les partenaires sont liaison hello entre Site Recovery et leurs clients. Les partenaires service relation de client hello et facturer les clients pour l’utilisation de la récupération de Site.

## <a name="create-and-manage-tenant-accounts"></a>Créer et gérer des comptes locataires

### <a name="step-0-prerequisite-check"></a>Étape 0 : Vérifier les prérequis

Hello conditions préalables de machine virtuelle sont hello identique à celle décrite dans hello [documentation Azure Site Recovery](site-recovery-vmware-to-azure.md). Dans les conditions préalables toothose de plus, vous doit avoir hello des contrôles d’accès mentionnées précédemment en place avant de continuer avec la gestion des clients via le fournisseur de services cryptographiques. Pour chaque client, créez un serveur d’administration distincts qui peut communiquer avec les machines virtuelles du locataire hello et vCenter du partenaire. Seuls les partenaires hello a serveur toothis de droits accès.

### <a name="step-1-create-a-tenant-account"></a>Étape 1 : Créer un compte locataire

1. Via [Microsoft Partner Center](https://partnercenter.microsoft.com/), connectez-vous au compte de fournisseur de services cryptographiques tooyour. 
 
2. Sur hello **tableau de bord** menu, sélectionnez **clients**.

    ![lien de clients de Microsoft Partner Center Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. Page hello qui s’ouvre, cliquez sur hello **ajouter un client** bouton.

    ![bouton Add Customer de Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. Sur hello **nouveau client** page, renseignez les informations de compte hello pour le client de hello, puis cliquez sur **suivant : abonnements**.

    ![page Hello compte](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. Sur la page de sélection hello abonnements, sélectionnez hello **Microsoft Azure** case à cocher. Vous pouvez ajouter d’autres abonnements maintenant ou à tout moment.

    ![case à cocher abonnement Hello Microsoft Azure](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. Sur hello **révision** page, vérifiez les détails des locataires hello, puis cliquez sur **Submit**.

    ![page vérifier la Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Une fois que vous avez créé le compte client hello, une page de confirmation s’affiche, affichage des détails de hello Hello compte par défaut hello de mot de passe pour cet abonnement. 

7. Enregistrer les informations de hello et modifiez le mot de passe hello ultérieurement selon les besoins via hello Azure portail-page de connexion.  
 
    Vous pouvez partager ces informations avec client hello en l’état, ou vous pouvez créer et partager un compte distinct, si nécessaire.

### <a name="step-2-access-hello-tenant-account"></a>Étape 2 : Le compte client hello accéder à

Vous pouvez accéder à hello l’abonnement du client via hello tableau de bord du centre de partenaires Microsoft, comme décrit dans « étape 1 : créer un compte client. » 

1. Accédez toohello **clients** page, puis cliquez sur nom hello du compte de locataire hello.

2. Sur hello **abonnements** page du compte de locataire hello, vous pouvez surveiller les abonnements de compte existant hello et ajouter plusieurs abonnements, en fonction des besoins. opérations de récupération d’urgence du locataire toomanage hello, sélectionnez **(portail Azure) de toutes les ressources**.

    ![lien de toutes les ressources Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    En cliquant sur **toutes les ressources** vous permet d’accéder les abonnements du locataire toohello Azure. Vous pouvez vérifier l’accès en cliquant sur le lien d’Azure Active Directory de hello en hello haut à droite de hello portail Azure.

    ![Lien Azure Active Directory](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

Vous pouvez maintenant effectuer toutes les opérations de récupération de site pour le client hello via hello portail Azure et gérer les opérations de récupération d’urgence hello. tooaccess l’abonnement client hello via le fournisseur de services cryptographiques pour la récupération d’urgence managé, suivez hello précédemment processus.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>Étape 3 : Déployer l’abonnement aux ressources toohello client
1. Sur hello portail Azure, créer un groupe de ressources et déployez ensuite un coffre Recovery Services par les processus habituel hello. 
 
2. Télécharger la clé d’inscription du coffre hello.

3. Inscrire CS hello pour le client de hello en utilisant la clé d’inscription du coffre hello.

4. Entrez des informations d’identification de hello hello deux comptes d’accès : compte d’accès vCenter compte d’accès et de la machine virtuelle.

    ![Comptes serveur de configuration de gestionnaire](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>Étape 4 : Infrastructure de la récupération de Site de Registre des Services de récupération toohello coffre
1. Dans hello portail Azure, sur le coffre hello que vous avez créé précédemment, inscrire hello vCenter server toohello CS que vous avez enregistré dans « étape 3 : déployer l’abonnement aux ressources de locataire toohello. » Utiliser le compte d’accès hello vCenter à cet effet.
2. Processus hello « Préparation infrastructure » pour la récupération de Site par les processus habituel hello.
3. Hello machines virtuelles sont désormais prêt toobe répliquée. Vérifiez que seuls hello machines virtuelles du locataire sont affichés sur hello **sélectionner des machines virtuelles** panneau sous hello **répliquer** option.

    ![Liste des ordinateurs virtuels sur le panneau de sélectionner les ordinateurs virtuels hello du locataire](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>Étape 5 : Affecter locataire accès toohello abonnement

Pour la récupération d’urgence de libre-service, fournir toohello client détails du compte hello, comme indiqué à l’étape 6 de hello « étape 1 : créer un compte client « section. Effectuer cette action une fois que le partenaire de hello configure infrastructure de récupération d’urgence hello. Si le type de récupération d’urgence hello est géré ou libre-service, partenaires doivent accéder aux abonnements du locataire via le portail de fournisseur de services cryptographiques hello. Ils configuration coffre appartenant à un partenaire de hello et inscrire des abonnements du locataire toohello infrastructure.

Partenaires peuvent également ajouter un nouvel abonnement client toohello utilisateur via le portail de fournisseur de services cryptographiques hello de manière hello suivante :

1. Atteindre la page d’abonnement du locataire toohello CSP et sélectionnez hello **utilisateurs et licences** option.

    ![page d’abonnement du locataire CSP de Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    Vous pouvez maintenant créer un nouvel utilisateur en entrant les détails pertinents hello et en sélectionnant des autorisations ou en téléchargeant la liste de hello des utilisateurs dans un fichier CSV.

2. Une fois que vous avez créé un nouvel utilisateur, revenir en arrière toohello Azure portail, puis, dans hello **abonnement** panneau, abonnement pertinentes de hello select.

3. Dans le panneau hello qui s’ouvre, sélectionnez **contrôle d’accès (IAM)**, puis cliquez sur **ajouter** tooadd un utilisateur avec le niveau d’accès hello.      
    Hello les utilisateurs qui ont été créés via le portail de fournisseur de services cryptographiques hello sont automatiquement affichés sur le panneau hello qui s’ouvre lorsque vous cliquez sur un niveau d’accès.

    ![Ajouter un utilisateur](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    Pour la plupart des opérations de gestion, hello *collaborateur* rôle est suffisant. Les utilisateurs disposant de ce niveau d’accès peuvent effectuer toutes les opérations sur un abonnement, à l’exception du changement de niveau d’accès (pour cette opération, le niveau d’accès *Propriétaire* est nécessaire). Vous pouvez également ajuster les niveaux d’accès hello en fonction des besoins.
