---
title: "aaaConfigure toujours sur le groupe de disponibilité dans des Machines virtuelles Azure (classique) | Documents Microsoft"
description: "Créez un groupe de disponibilité Always On avec des machines virtuelles Azure. Ce didacticiel utilise principalement de l’interface utilisateur hello et outils plutôt que de script."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>Configuration d’un groupe de disponibilité Always On dans des machines virtuelles Azure (Classic)
> [!div class="op_single_selector"]
> * [Classic : interface utilisateur](../classic/portal-sql-alwayson-availability-groups.md)
> * [Classic : PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Avant de commencer, rappelez-vous que vous pouvez accomplir cette tâche dans le modèle Azure Resource Manager. Nous vous recommandons d’utiliser le modèle Azure Resource Manager pour les nouveaux déploiements. Consultez [Présentation des groupes de disponibilité SQL Server AlwaysOn sur des machines virtuelles Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT] 
> Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Azure propose deux toocreate de modèles de déploiement différentes et utiliser des ressources : [le Gestionnaire de ressources et classic](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article explique comment toouse hello modèle de déploiement classique. 

reportez-vous à cette tâche avec le modèle de gestionnaire de ressources Azure hello, toocomplete [groupes de disponibilité SQL Server Always On sur des machines virtuelles](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

Ce didacticiel de bout en bout illustre la façon dont les groupes tooimplement disponibilité à l’aide de SQL Server Always On en cours d’exécution sur des Machines virtuelles Azure.

À la fin de hello du didacticiel de hello, votre solution SQL Server Always On dans Azure comprendra hello suivant d’éléments :

* un réseau virtuel contenant plusieurs sous-réseaux, notamment un sous-réseau frontal et un sous-réseau principal ;
* un contrôleur de domaine avec un domaine Active Directory (Azure AD) ;
* Deux ordinateurs virtuels qui exécutent SQL Server et qui sont déployés toohello principal sous-réseau et du domaine de toohello jointes Azure AD
* Un cluster de basculement de trois nœuds avec le modèle de quorum nœud majoritaire hello
* un groupe de disponibilité avec deux réplicas avec validation synchrone d’une base de données de disponibilité.

Hello après l’illustration est une représentation graphique de la solution de hello.

![Architecture de laboratoire de test pour les groupes de disponibilité dans Azure](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

Notez qu'il s'agit d'une configuration possible. Par exemple, vous pouvez réduire nombre hello d’ordinateurs virtuels pour un groupe de disponibilité de deux réplicas. Cette configuration permet d’économiser sur les heures de calcul dans Azure à l’aide du contrôleur de domaine hello en tant que témoin de partage de fichiers hello quorum dans un cluster à deux nœuds. Cette méthode réduit le nombre d’ordinateurs virtuels hello par rapport à la configuration de hello illustré.

Ce didacticiel suppose hello qui suit :

* Vous disposez déjà d’un compte Azure.
* Vous savez déjà comment toouse hello GUI dans tooprovision de la galerie de machine virtuelle hello, un ordinateur virtuel classique qui exécute SQL Server.
* Vous disposez déjà d’une connaissance approfondie des groupes de disponibilité Always On. Pour plus d’informations, voir [Groupes de disponibilité AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Si l’utilisation des groupes de disponibilité Always On avec SharePoint vous intéresse, consultez [Configurer des groupes de disponibilité AlwaysOn SQL Server 2012 pour SharePoint 2013](https://technet.microsoft.com/library/jj715261.aspx).
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Créer le réseau virtuel de hello et serveur contrôleur de domaine
Vous commencez avec un nouveau compte d'essai Azure. Après avoir configuré votre compte, vous devez être sur l’écran d’accueil hello Hello portail Azure classic.

1. Cliquez sur hello **nouveau** situé à gauche du bas hello de page hello, comme indiqué dans hello suivant capture d’écran hello.
   
    ![Cliquez sur Nouveau dans le portail de hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. Cliquez sur **Services réseau** > **réseau virtuel** > **création personnalisée**, comme indiqué dans hello suivant capture d’écran.
   
    ![Créer un réseau virtuel](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. Bonjour **créer un réseau virtuel** boîte de dialogue zone, créez un réseau virtuel en parcourant les pages hello et à l’aide des paramètres de hello Bonjour tableau suivant. 
   
   | Page | Paramètres |
   | --- | --- |
   | Détails du réseau virtuel |**NOM = ContosoNET**<br/>**REGION = West US** |
   | Serveurs DNS et connectivité VPN |Aucun |
   | Espaces d’adressage du réseau virtuel |Les paramètres sont indiqués dans hello suivant capture d’écran : ![Créer un réseau virtuel](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Créer un ordinateur virtuel hello que vous utiliserez en tant que contrôleur de domaine hello (DC). Cliquez sur **nouveau** > **de calcul** > **virtuels** > **à partir de la galerie**, comme indiqué dans Hello suivant capture d’écran.
   
    ![Création d'une machine virtuelle](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. Bonjour **créer une MACHINE virtuelle** boîte de dialogue zone, configurer une machine virtuelle en parcourant les pages hello et à l’aide des paramètres de hello Bonjour tableau suivant. 
   
   | Page | Paramètres |
   | --- | --- |
   | Sélectionnez le système d’exploitation de machine virtuelle hello |Windows Server 2012 R2 Datacenter |
   | Configuration de la machine virtuelle |**DATE DE SORTIE DE LA VERSION** = (dernière version)<br/>**NOM DE LA MACHINE VIRTUELLE** = ContosoDC<br/>**NIVEAU** = STANDARD<br/>**TAILLE** = A2 (2 cœurs)<br/>**NOUVEAU NOM D'UTILISATEUR** = AzureAdmin<br/>**NOUVEAU MOT DE PASSE** = Contoso!000<br/>**CONFIRM** = Contoso!000 |
   | Configuration de la machine virtuelle |**SERVICE CLOUD** = créez un service cloud<br/>**NOM DNS DU SERVICE CLOUD** = un nom de service cloud unique<br/>**NOM DNS** = un nom unique (ex : ContosoDC123)<br/>**RÉGION/GROUPE D'AFFINITÉ/RÉSEAU VIRTUEL** = ContosoNET<br/>**SOUS-RÉSEAUX VIRTUELS** = Back(10.10.2.0/24)<br/>**COMPTE DE STOCKAGE** : utilisez un compte de stockage généré automatiquement<br/>**AVAILABILITY SET** = (Aucun) |
   | Options de la machine virtuelle |Utilisation des valeurs par défaut |

Après avoir configuré la machine virtuelle hello, attendez la mise en service des toobe hello machine virtuelle. Ce processus prend quelques toofinish de temps. Si vous cliquez sur hello **Machine virtuelle** onglet Bonjour Azure classic portail, vous pouvez voir États ContosoDC casquettes **départ (Provisioning)** trop**arrêté**, **Démarrage**, **en cours d’exécution (approvisionnement)**et enfin **en cours d’exécution**.

serveur de contrôleur de domaine Hello est maintenant correctement configuré. Ensuite, vous allez configurer le domaine d’Active Directory hello sur ce serveur de contrôleur de domaine.

## <a name="configure-hello-domain-controller"></a>Configurer le contrôleur de domaine hello
Bonjour comme suit, vous configurez machine ContosoDC de hello en tant que contrôleur de domaine pour corp.contoso.com.

1. Dans le portail de hello, sélectionnez hello **ContosoDC** machine. Sur hello **tableau de bord** , cliquez sur **Connect** tooopen un bureau à distance (RDP) du fichier pour l’accès Bureau à distance.
   
    ![Se connecter tooVritual Machine](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. Connectez-vous avec votre compte administrateur configuré (**\AzureAdmin**) et votre mot de passe (**Contoso!000**).
3. Par défaut, hello **le Gestionnaire de serveur** tableau de bord doit être affiché.
4. Cliquez sur hello **ajouter des rôles et fonctionnalités** lien sur le tableau de bord hello.
   
    ![Ajout de rôles Explorateur de serveurs](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. Cliquez sur **suivant** jusqu'à ce que vous atteigniez toohello **rôles serveur** section.
6. Sélectionnez hello **les Services de domaine Active Directory** et **serveur DNS** rôles. Lorsque vous y êtes invité, ajoutez d’autres fonctionnalités nécessaires pour ces rôles.
   
   > [!NOTE]
   > Vous obtiendrez un avertissement de validation vous informant qu'il n’y a aucune adresse IP statique. Si vous testez la configuration de hello, cliquez sur **continuer**. Pour les scénarios de production [utiliser PowerShell tooset hello adresse IP de l’ordinateur du contrôleur de domaine hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   > 
   > 
   
    ![Boîte de dialogue Ajouter des rôles](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. Cliquez sur **suivant** jusqu'à ce que vous atteigniez hello **Confirmation** section. Sélectionnez hello **redémarrez le serveur de destination hello automatiquement si nécessaire** case à cocher.
8. Cliquez sur **Installer**.
9. Une fois que les fonctions hello sont installées, retourner toohello **le Gestionnaire de serveur** tableau de bord.
10. Sélectionnez hello nouvelle **AD DS** option dans le volet gauche de hello.
11. Cliquez sur hello **plus** lien dans la barre d’avertissement jaune de hello.
    
     ![Boîte de dialogue AD DS sur une machine virtuelle du serveur DNS](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. Bonjour **Action** colonne Hello **tous les détails de la tâche serveur** boîte de dialogue, cliquez sur **promouvoir ce serveur de contrôleur de domaine tooa**.
13. Bonjour **Assistant Configuration de Services de domaine Active Directory**, utilisez hello valeurs suivantes :
    
    | Page | Paramètre |
    | --- | --- |
    | Configuration du déploiement |**Ajouter une nouvelle forêt** = sélectionné<br/>**Nom de domaine racine** = corp.contoso.com |
    | Options de contrôleur de domaine : |**Mot de passe** = Contoso!000<br/>**Confirmer le mot de passe** = Contoso!000 |
14. Cliquez sur **suivant** toogo via hello autres pages de l’Assistant de hello. Sur hello **vérification** , vérifiez que vous consultez hello message suivant : **toutes les vérifications des conditions préalables a réussi**. Notez que vous devez passer en revue tous les messages d’avertissement applicables, mais il est possible de toocontinue avec l’installation de hello.
15. Cliquez sur **Installer**. Hello **ContosoDC** ordinateur virtuel redémarre automatiquement.

## <a name="configure-domain-accounts"></a>Configurer les comptes de domaine
étapes Hello configurent des comptes Active Directory de hello pour une utilisation ultérieure.

1. Se reconnecter toohello **ContosoDC** machine.
2. Dans **Gestionnaire de serveur**, cliquez sur **Outils** > **Centre d’administration Active Directory**.
   
    ![Centre d'administration Active Directory](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. Bonjour **centre d’administration Active Directory**, sélectionnez **corp (local)** dans le volet gauche de hello.
4. Sur la droite de hello **tâches** volet, cliquez sur **nouveau** > **utilisateur**. Utilisez hello suivant les paramètres :
   
   | Paramètre | Valeur |
   | --- | --- |
   | **Prénom** |Installer |
   | **SamAccountName de l'utilisateur** |Installer |
   | **Mot de passe** |Contoso!000 |
   | **Confirmer le mot de passe** |Contoso!000 |
   | **Autres options de mot de passe** |Sélectionné |
   | **Le mot de passe n'expire jamais** |Activé |
5. Cliquez sur **OK** toocreate hello **installer** utilisateur. Ce compte sera utilisé tooconfigure hello basculement cluster et hello groupe de disponibilité.
6. Créez deux utilisateurs supplémentaires, **CORP\SQLSvc1** et **CORP\SQLSvc2**, avec hello mêmes étapes. Ces comptes seront utilisés pour les instances de SQL Server hello. Ensuite, vous devez toogive **CORP\Install** hello clustering de basculement de Windows tooconfigure les autorisations nécessaires.
7. Bonjour **centre d’administration Active Directory**, cliquez sur **corp (local)** dans le volet gauche de hello. Bonjour **tâches** volet, cliquez sur **propriétés**.
   
    ![Propriétés de l’utilisateur CORP](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. Sélectionnez **Extensions**, puis cliquez sur hello **avancé** bouton sur hello **sécurité** onglet.
9. Bonjour **des paramètres de sécurité avancés pour corp** boîte de dialogue, cliquez sur **ajouter**.
10. Cliquez sur **Sélectionnez un principal**, recherchez **CORP\Install**, puis cliquez sur **OK**.
11. Sélectionnez hello **lire toutes les propriétés** et **Créer objets ordinateur** autorisations.
    
     ![Autorisations de l’utilisateur Corp](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. Cliquez sur **OK**, puis sur **OK** à nouveau. Fenêtre Propriétés de corp hello fermer.

Maintenant que vous avez configuré Active Directory et les objets utilisateur hello, vous créez trois machines virtuelles de SQL Server et les attacher toothis domaine.

## <a name="create-hello-sql-server-virtual-machines"></a>Créer des machines virtuelles SQL Server hello
Créez trois machines virtuelles. La première est utilisée pour un nœud de cluster, les deux autres pour SQL Server. toocreate d’ordinateurs virtuels de hello, allez sauvegarder toohello portail Azure classic, cliquez sur **nouveau** > **de calcul** > **virtuels**  >  **à partir de la galerie**. Ensuite, utilisez les modèles de hello hello suivant toohelp table vous créez des machines virtuelles de hello.

| Page | MV1 | MV2 | MV3 |
| --- | --- | --- | --- |
| Sélectionnez le système d’exploitation de machine virtuelle hello |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| Configuration de la machine virtuelle |**DATE DE SORTIE DE LA VERSION** = (dernière version)<br/>**NOM DE LA MACHINE VIRTUELLE** = ContosoWSFCNode<br/>**NIVEAU** = STANDARD<br/>**TAILLE** = A2 (2 cœurs)<br/>**NOUVEAU NOM D'UTILISATEUR** = AzureAdmin<br/>**NOUVEAU MOT DE PASSE** = Contoso!000<br/>**CONFIRM** = Contoso!000 |**DATE DE SORTIE DE LA VERSION** = (dernière version)<br/>**NOM DE LA MACHINE VIRTUELLE** = ContosoSQL1<br/>**NIVEAU** = STANDARD<br/>**TAILLE** = A3 (4 cœurs)<br/>**NOUVEAU NOM D'UTILISATEUR** = AzureAdmin<br/>**NOUVEAU MOT DE PASSE** = Contoso!000<br/>**CONFIRM** = Contoso!000 |**DATE DE SORTIE DE LA VERSION** = (dernière version)<br/>**NOM DE LA MACHINE VIRTUELLE** = ContosoSQL2<br/>**NIVEAU** = STANDARD<br/>**TAILLE** = A3 (4 cœurs)<br/>**NOUVEAU NOM D'UTILISATEUR** = AzureAdmin<br/>**NOUVEAU MOT DE PASSE** = Contoso!000<br/>**CONFIRM** = Contoso!000 |
| Configuration de la machine virtuelle |**SERVICE CLOUD** = nom DNS du service cloud unique créé précédemment (ex : ContosoDC123)<br/>**RÉGION/GROUPE D'AFFINITÉ/RÉSEAU VIRTUEL** = ContosoNET<br/>**SOUS-RÉSEAUX VIRTUELS** = Back(10.10.2.0/24)<br/>**COMPTE DE STOCKAGE** : utilisez un compte de stockage généré automatiquement<br/>**GROUPE À HAUTE DISPONIBILITÉ** = Créez un groupe à haute disponibilité<br/>**AVAILABILITY SET NAME** = SQLHADR |**SERVICE CLOUD** = nom DNS du service cloud unique créé précédemment (ex : ContosoDC123)<br/>**RÉGION/GROUPE D'AFFINITÉ/RÉSEAU VIRTUEL** = ContosoNET<br/>**SOUS-RÉSEAUX VIRTUELS** = Back(10.10.2.0/24)<br/>**COMPTE DE STOCKAGE** : utilisez un compte de stockage généré automatiquement<br/>**HAUTE disponibilité** = SQLHADR (vous pouvez également configurer disponibilité hello après hello machine a été créée. Les trois ordinateurs doivent être assignées à haute disponibilité SQLHADR toohello.) |**SERVICE CLOUD** = nom DNS du service cloud unique créé précédemment (ex : ContosoDC123)<br/>**RÉGION/GROUPE D'AFFINITÉ/RÉSEAU VIRTUEL** = ContosoNET<br/>**SOUS-RÉSEAUX VIRTUELS** = Back(10.10.2.0/24)<br/>**COMPTE DE STOCKAGE** : utilisez un compte de stockage généré automatiquement<br/>**HAUTE disponibilité** = SQLHADR (vous pouvez également configurer disponibilité hello après hello machine a été créée. Les trois ordinateurs doivent être assignées à haute disponibilité SQLHADR toohello.) |
| Options de la machine virtuelle |Utilisation des valeurs par défaut |Utilisation des valeurs par défaut |Utilisation des valeurs par défaut |

<br/>

> [!NOTE]
> configuration précédente de Hello suggère des ordinateurs virtuels de niveau STANDARD, car les ordinateurs de niveau de base ne prennent pas en charge les points de terminaison avec équilibrage de charge. Vous avez besoin de points de terminaison avec équilibrage de charge ultérieure toocreate un écouteur de groupe de disponibilité. En outre, les tailles de machine hello qui sont suggérés ici sont destinées pour le test des groupes de disponibilité dans Azure Virtual Machines. Pour des performances optimales hello sur les charges de production, voir les recommandations de hello pour les tailles d’ordinateur SQL Server et la configuration dans [performances meilleures pratiques pour SQL Server dans Azure Virtual Machines](../sql/virtual-machines-windows-sql-performance.md).
> 
> 

Une fois hello trois ordinateurs virtuels sont entièrement configurés, vous devez toojoin les toohello **corp.contoso.com** domaine et allocation de machines toohello à CORP\Install des droits d’administration. toodo, hello utilisation comme suit pour chacun des ordinateurs virtuels hello trois.

1. Tout d’abord, modifiez adresse du serveur DNS préféré de hello. Télécharger le répertoire local de chaque ordinateur virtuel RDP fichier tooyour en sélectionnant des ordinateurs virtuels de hello dans la liste de hello en cliquant hello **Connect** bouton. tooselect un ordinateur virtuel, cliquez sur n’importe où mais hello première cellule de ligne de hello, comme indiqué dans hello suivant capture d’écran.
   
    ![Téléchargement du fichier RDP de hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. Ouvrez hello RDP fichier que vous avez téléchargé et connectez-vous à toohello virtuels à l’aide de votre compte d’administrateur configuré (**BUILTIN\AzureAdmin**) et le mot de passe (**Contoso ! 000**).
3. Après vous être connecté, vous devez voir hello **le Gestionnaire de serveur** tableau de bord. Cliquez sur **serveur Local** dans le volet gauche de hello.
4. Cliquez sur hello **adresse IPv4 attribuée par DHCP, compatible IPv6** lien.
5. Bonjour **connexions réseau** boîte de dialogue, cliquez sur icône du réseau hello.
   
    ![Modifier le serveur DNS d’ordinateur virtuel par défaut hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Dans la barre de commandes hello, cliquez sur **modifier les paramètres de cette connexion de hello**. (Selon la taille de hello de votre fenêtre, vous devez peut-être tooclick hello double flèche droite toosee cette commande).
7. Cliquez sur **Internet Protocol Version 4 (TCP/IPv4)**, puis sur **Propriétés**.
8. Sélectionnez **hello utilisation suivant des adresses de serveur DNS** , puis spécifiez **10.10.2.4** dans **serveur DNS préféré**.
9. Hello **10.10.2.4** adresse est hello qui tooa attribué virtual machine est dans le sous-réseau 10.10.2.0/24 de hello dans un réseau virtuel Azure. Cette machine virtuelle est **ContosoDC**. tooverify **ContosoDC**d’adresse IP, utilisez **nslookup contosodc** dans la fenêtre d’invite de commandes hello, comme indiqué dans hello suivant capture d’écran.
   
    ![Utilisez l’adresse IP de toofind NSLOOKUP pour le contrôleur de domaine](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. Cliquez sur **OK** > **fermer** modifications de hello toocommit. Vous pouvez désormais joindre hello virtual machine trop**corp.contoso.com**.
11. Dans hello **serveur Local** fenêtre, cliquez sur hello **groupe de travail** lien.
12. Bonjour **nom de l’ordinateur** , cliquez sur **modification**.
13. Sélectionnez hello **domaine** case à cocher, tapez **corp.contoso.com** dans hello de zone de texte, puis cliquez sur **OK**.
14. Bonjour **sécurité Windows** boîte de dialogue, spécifiez les informations d’identification hello pour le compte d’administrateur par défaut hello (**CORP\AzureAdmin**) et le mot de passe hello (**Contoso ! 000**).
15. Lorsque vous voyez le message de salutation « domaine corp.contoso.com de bienvenue toohello », cliquez sur **OK**.
16. Cliquez sur **fermer** > **redémarrer maintenant** dans la boîte de dialogue hello.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>Ajouter un utilisateur de Corp\Install hello en tant qu’administrateur sur chaque ordinateur virtuel
1. Attendez que le redémarrage de la machine virtuelle hello et puis ouvrez hello RDP fichier toosign dans la machine virtuelle de toohello à l’aide de hello **BUILTIN\AzureAdmin** compte.
2. Dans **Gestionnaire de serveur**, cliquez sur **Outils** > **Gestion de l’ordinateur**.
   
    ![Gestion de l'ordinateur](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. Bonjour **gestion de l’ordinateur** boîte de dialogue, développez **utilisateurs et groupes locaux**, puis cliquez sur **groupes**.
4. Double-cliquez sur hello **administrateurs** groupe.
5. Bonjour **propriétés du groupe Administrateurs** boîte de dialogue, cliquez sur hello **ajouter** bouton.
6. Entrez hello utilisateur **CORP\Install**, puis cliquez sur **OK**. Lorsque vous y êtes invité pour les informations d’identification, utilisez hello **AzureAdmin** compte avec hello **Contoso ! 000** mot de passe.
7. Cliquez sur **OK** tooclose hello **propriétés de l’administrateur** boîte de dialogue.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Ajouter le Clustering de basculement de hello machine virtuelle tooeach à fonctionnalité
1. Bonjour **le Gestionnaire de serveur** tableau de bord, cliquez sur **ajouter des rôles et fonctionnalités**.
2. Bonjour **Assistant Ajouter des rôles et fonctionnalités**, cliquez sur **suivant** jusqu'à ce que vous atteigniez toohello **fonctionnalités** page.
3. Sélectionnez **Clustering de basculement**. Lorsque vous y êtes invité, ajoutez les autres fonctionnalités dépendantes.
   
    ![Ajouter la fonctionnalité de Clustering de basculement toovirtual machine](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. Cliquez sur **suivant**, puis cliquez sur **installer** sur hello **Confirmation** page.
5. Hello lorsque **le Clustering de basculement** installation de fonctionnalités est terminée, cliquez sur **fermer**.
6. Déconnectez-vous de machine virtuelle de hello.
7. Répétez les étapes de cette section pour les trois serveurs hello : **ContosoWSFCNode**, **ContosoSQL1**, et **ContosoSQL2**.

Hello SQL Server, les ordinateurs virtuels sont maintenant configurés et en cours d’exécution, mais chacune a des options par défaut de hello pour SQL Server.

## <a name="create-hello-failover-cluster"></a>Créer le cluster de basculement hello
Dans cette section, vous créez cluster de basculement hello qui va héberger le groupe de disponibilité hello que vous créerez ultérieurement. À ce stade, vous devriez avoir effectué hello suivant tooeach d’ordinateurs virtuels hello trois que vous utiliserez dans un cluster de basculement hello :

* Machine virtuelle de hello entièrement dans Azure
* Joints à un domaine de toohello hello machine virtuelle
* Ajouté **CORP\Install** toohello groupe d’administrateurs locaux
* Fonctionnalité de clustering de basculement hello ajouté

Il s’agit des composants requis sur chaque ordinateur virtuel avant de joindre cluster de basculement toohello.

En outre, notez que hello réseau virtuel Azure ne comporte pas de hello même manière qu’un réseau local. Vous avez besoin de cluster de hello toocreate Bonjour suivant l’ordre :

1. Création d’un cluster à nœud unique sur un seul nœud (**ContosoSQL1**).
2. Modifier hello cluster IP adresse tooan adresse IP inutilisée (**10.10.2.101**).
3. Mettez le nom du cluster hello en ligne.
4. Ajouter hello autres nœuds (**ContosoSQL2** et **ContosoWSFCNode**).

Utilisez hello suivant les étapes toocomplete hello tâches que configurer complètement le cluster de hello.

1. Fichier RDP de hello ouvert pour **ContosoSQL1**et vous connecter à l’aide du compte de domaine hello **CORP\Install**.
2. Bonjour **le Gestionnaire de serveur** tableau de bord, cliquez sur **outils** > **Gestionnaire du Cluster de basculement**.
3. Dans le volet gauche de hello, cliquez sur **Gestionnaire du Cluster de basculement**, puis cliquez sur **créer un Cluster**, comme indiqué dans hello suivant capture d’écran.
   
    ![Créer un cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. Dans hello Assistant Création d’un Cluster, créez un cluster à un nœud en parcourant les pages hello et à l’aide des paramètres de hello Bonjour tableau suivant :
   
   | Page | Paramètres |
   | --- | --- |
   | Avant de commencer |Utilisation des valeurs par défaut |
   | Sélection des serveurs |Tapez **ContosoSQL1** dans **Entrez le nom du serveur**, puis cliquez sur **Ajouter** |
   | Avertissement de validation |Sélectionnez **non. je ne nécessitent pas de prise en charge de Microsoft pour ce cluster et par conséquent ne voulez pas que la validation toorun hello teste. Lorsque vous cliquez sur Suivant, poursuivre la création de cluster de hello**. |
   | Point d’accès pour administration hello Cluster |Saisissez **Cluster1** dans **Nom du cluster**. |
   | Confirmation |Utilisez les valeurs par défaut, sauf si vous utilisez des espaces de stockage. Consultez l’avertissement hello sous ce tableau. |
   
   > [!WARNING]
   > Si vous utilisez [des espaces de stockage](https://technet.microsoft.com/library/hh831739), qui regroupe plusieurs disques dans des pools de stockage, vous devez effacer hello **ajouter tous les totalité du stockage du cluster toohello** case à cocher sur hello **Confirmation** page. Si vous ne désactivez pas cette option, les disques virtuels hello sont détachés pendant hello processus de clustering. Par conséquent, elles seront également apparaissent pas dans le Gestionnaire de disque ou de l’Explorateur jusqu'à ce que les espaces de stockage hello sont supprimés du cluster de hello et rattachés à l’aide de PowerShell.
   > 
   > 
5. Dans le volet gauche de hello, développez **Gestionnaire du Cluster de basculement**, puis cliquez sur **Cluster1.corp.contoso.com**.
6. Dans le volet central de hello, faites défiler vers le bas toohello **ressources principales du Cluster** section et développez hello **nom : Clutser1** détails. Vous devez voir deux hello **nom** et hello **adresse IP** ressources Bonjour **n’a pas pu** état. Hello ressource d’adresse IP ne peut pas être mises en ligne, car le cluster de hello a hello même adresse IP en tant qu’ordinateur hello lui-même, qui est une adresse en double.
7. Hello avec le bouton échoué **adresse IP** ressource, puis cliquez sur **propriétés**.
   
    ![Propriétés du cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. Sélectionnez **adresse IP statique**, spécifiez **10.10.2.101** Bonjour **adresse** zone de texte, puis cliquez sur **OK**.
9. Bonjour **ressources principales du Cluster** section, cliquez sur **nom : Cluster1**, puis cliquez sur **mettre en ligne**. Attendez que les deux ressources soient en ligne. Lors de la ressource de nom de cluster hello est mis en ligne, serveur de contrôleur de domaine hello est mise à jour avec un nouveau compte d’ordinateur Active Directory. Ce compte Active Directory sera utilisé toorun hello du groupe de disponibilité service en cluster ultérieurement.
10. Ajoutez hello restants du cluster toohello de nœuds. Dans l’arborescence du navigateur hello, cliquez sur **Cluster1.corp.contoso.com**, puis cliquez sur **ajouter un nœud**, comme indiqué dans hello suivant capture d’écran.
    
     ![Ajouter un nœud toohello cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. Bonjour **Assistant Ajout de nœud**, cliquez sur **suivant** sur hello **sélectionner des serveurs** , ajoutez **ContosoSQL2** et **ContosoWSFCNode**  liste toohello en tapant le nom du serveur hello dans **nom du serveur** , puis en cliquant sur **ajouter**. Une fois ces opérations effectuées, cliquez sur **Suivant**.
12. Sur hello **avertissement de Validation** , cliquez sur **non**, bien que dans un scénario de production, vous devez effectuer des tests de validation hello. Cliquez ensuite sur **Suivant**.
13. Sur hello **Confirmation** , cliquez sur **suivant** nœuds de hello tooadd.
    
    > [!WARNING]
    > Si vous utilisez [des espaces de stockage](https://technet.microsoft.com/library/hh831739), qui regroupe plusieurs disques dans des pools de stockage, vous devez effacer hello **ajouter tous les totalité du stockage du cluster toohello** case à cocher. Si vous ne désactivez pas cette option, les disques virtuels hello sont détachés pendant hello processus de clustering. Par conséquent, ils pas apparaîtra également dans le Gestionnaire de disque ou de l’Explorateur jusqu'à ce que les espaces de stockage hello sont supprimés du cluster et rattachés à l’aide de PowerShell.
    > 
    > 
14. Après l’ajout de nœuds de hello toohello cluster, cliquez sur **Terminer**. Gestionnaire du Cluster de basculement devrait maintenant indiquer que votre cluster a trois nœuds et les répertorier dans hello **nœuds** conteneur.
15. Déconnectez-vous de session Bureau à distance de hello.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>Préparer des instances de SQL Server hello pour les groupes de disponibilité
Dans cette section, vous ferez hello suivant sur les deux **ContosoSQL1** et **contosoSQL2**:

* Ajouter un compte de connexion pour **NT AUTHORITY\System** avec les autorisations requises définir l’instance de SQL Server toohello par défaut.
* Ajouter **CORP\Install** comme une instance de SQL Server sysadmin rôle toohello par défaut.
* Ouvrez le pare-feu hello pour l’accès à distance de SQL Server.
* Activez hello Always On fonctionnalité de groupes de disponibilité.
* Modifier le compte de service SQL Server hello trop**CORP\SQLSvc1** et **CORP\SQLSvc2**, respectivement.

Ces actions peuvent être effectuées dans n'importe quel ordre. Néanmoins, hello suit habituel dans l’ordre. Suivez les étapes de hello pour les deux **ContosoSQL1** et **ContosoSQL2**:

1. Si vous n’êtes pas connecté en dehors de la session Bureau à distance de hello pour la machine virtuelle de hello, faites-le maintenant.
2. Ouvrez hello RDP fichiers pour **ContosoSQL1** et **ContosoSQL2**, connectez-vous en tant que **BUILTIN\AzureAdmin**.
3. Ajouter **NT AUTHORITY\System** toohello les connexions de SQL Server avec les autorisations requises. Ouvrez **SQL Server Management Studio**.
4. Cliquez sur **Connect** instance de SQL Server tooconnect toohello par défaut.
5. Dans l’**Explorateur d’objets**, développez **Sécurité**, puis **Connexions**.
6. Avec le bouton hello **NT AUTHORITY\System** connexion, puis cliquez sur **propriétés**.
7. Sur hello **éléments sécurisables** page, hello local serveur, sélectionnez **Grant** pour hello les autorisations suivantes, puis cliquez sur **OK**.
   
   * Modifier un groupe de disponibilité
   * Connecter SQL
   * Afficher l’état du serveur
8. Ajouter **CORP\Install** comme un **sysadmin** instance de rôle toohello par défaut SQL Server. Dans **l’Explorateur d’objets**, cliquez avec le bouton droit sur **Connexions**, puis cliquez sur **Nouvelle connexion**.
9. Saisissez **CORP\Install** dans **Nom de connexion**.
10. Sur hello **rôles serveur** page, sélectionnez **sysadmin**, puis cliquez sur **OK**. Après avoir créé la connexion de hello, vous pouvez l’afficher en développant **connexions** dans **l’Explorateur d’objets**.
11. toocreate une règle de pare-feu pour SQL Server, sur hello **Démarrer** écran, ouvrez **pare-feu Windows avec fonctions avancées de sécurité**.
12. Dans le volet gauche de hello, sélectionnez **règles de trafic entrant**. Dans le volet droit de hello, cliquez sur **nouvelle règle**.
13. Sur hello **le Type de règle** , cliquez sur **programme** > **suivant**.
14. Sur hello **programme** page, sélectionnez **ce chemin d’accès du programme**, type **%ProgramFiles%\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** dans hello de zone de texte, puis cliquez sur **suivant**. Si vous suivez ces instructions sont à l’aide de SQL Server 2012, le répertoire de SQL Server hello est **MSSQL11. MSSQLSERVER**.
15. Sur hello **Action** page, conservez **autoriser la connexion hello** sélectionné, puis cliquez sur **suivant**.
16. Sur hello **profil** page, acceptez les paramètres par défaut de hello et puis cliquez sur **suivant**.
17. Sur hello **nom** , spécifiez un nom de la règle, tel que **SQL Server (règle de programme)**, Bonjour **nom** texte zone, puis cliquez sur **Terminer**.
18. tooenable hello **groupes de disponibilité AlwaysOn** fonctionnalité, sur hello **Démarrer** écran, ouvrez **Gestionnaire de Configuration SQL Server**.
19. Dans l’arborescence du navigateur hello, cliquez sur **SQL Server Services**, avec le bouton hello **SQL Server (MSSQLSERVER)** de service, puis cliquez sur **propriétés**.
20. Cliquez sur hello **haute disponibilité Always On** onglet, sélectionnez **activer groupes de disponibilité AlwaysOn**, comme indiqué dans hello après la capture d’écran, puis cliquez sur **appliquer**. Cliquez sur **OK** hello boîte de dialogue et ne fermez pas hello **propriétés** encore la boîte de dialogue. Vous allez redémarrer le service SQL Server de hello après avoir modifié le compte de service hello.
    
     ![Activer des groupes de disponibilité Always On](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. toochange hello compte de service SQL Server, cliquez sur hello **session** , tapez **CORP\SQLSvc1** (pour **ContosoSQL1**) ou **CORP\SQLSvc2** () pour **ContosoSQL2**) dans **nom de compte**, renseignez et confirmer le mot de passe hello, puis cliquez sur **OK**.
22. Dans la boîte de dialogue hello qui s’ouvre, cliquez sur **Oui** toorestart hello service SQL Server. Après le redémarrage de hello service SQL Server, modifications que vous avez apportées dans hello **propriétés** boîte de dialogue sont efficaces.
23. Déconnectez-vous des machines virtuelles de hello.

## <a name="create-hello-availability-group"></a>Créer le groupe de disponibilité hello
Vous êtes maintenant prêt tooconfigure un groupe de disponibilité. Voici une présentation des opérations à effectuer :

* Création d’une base de données (**MyDB1**) sur **ContosoSQL1**.
* Effectuer une sauvegarde complète et une sauvegarde du journal des transactions de base de données hello.
* Restaurer hello complète et de sauvegardes de journaux trop**ContosoSQL2** avec hello **NORECOVERY** option.
* Créer le groupe de disponibilité hello (**AG1**) avec validation synchrone, le basculement automatique et réplicas secondaires lisibles.

### <a name="create-hello-mydb1-database-on-contososql1"></a>Créer la base de données hello MyDB1 sur ContosoSQL1
1. Si vous n’avez pas déjà été déconnecté des sessions Bureau à distance de hello pour **ContosoSQL1** et **ContosoSQL2**, faites-le maintenant.
2. Fichier RDP de hello ouvert pour **ContosoSQL1**, connectez-vous en tant que **CORP\Install**.
3. Dans **l’Explorateur de fichiers**, sous **\\C:**, créez un répertoire appelé **sauvegarde**. Vous allez utiliser cette tooback active et restaurer votre base de données.
4. Cliquez sur le nouveau répertoire de hello, pointez trop**partager avec**, puis cliquez sur **des personnes spécifiques**, comme indiqué dans hello suivant capture d’écran.
   
    ![Créer un dossier de sauvegarde](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. Ajouter **CORP\SQLSvc1**, puis attribuez-lui hello **en lecture/écriture** autorisation. Ajouter **CORP\SQLSvc2**, puis attribuez-lui hello **en lecture** autorisation, comme indiqué dans hello après la capture d’écran, puis cliquez sur **partage**. Une fois hello au partage de fichiers est terminée, cliquez sur **fait**.
   
    ![Accorder des autorisations pour le dossier de sauvegarde](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. toocreate hello base de données à partir de hello **Démarrer** menu, ouvrir **SQL Server Management Studio**, puis cliquez sur **Connect** instance de SQL Server tooconnect toohello par défaut.
7. Dans **l’Explorateur d’objets**, cliquez avec le bouton droit sur **Bases de données**, puis cliquez sur **Nouvelle base de données**.
8. Dans **Nom de base de données**, saisissez **MyDB1**, puis cliquez sur **OK**.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>Effectuer une sauvegarde complète de MyDB1 et la restaurer sur ContosoSQL2
1. toomake une sauvegarde complète de hello de base de données, en **l’Explorateur d’objets**, développez **bases de données**, avec le bouton droit **MyDB1**, pointez trop**tâches**, et puis cliquez sur **Back Up**.
2. Bonjour **Source** section, conservez **type de sauvegarde** défini trop**complète**. Bonjour **Destination** , cliquez sur **supprimer** chemin tooremove hello par défaut pour le fichier de sauvegarde hello.
3. Bonjour **Destination** , cliquez sur **ajouter**.
4. Bonjour **nom de fichier** zone de texte, tapez  **\\ContosoSQL1\backup\MyDB1.bak**, cliquez sur **OK**, puis cliquez sur **OK** à nouveau tooback base de données hello. Fin de l’opération de sauvegarde hello, cliquez sur **OK** tooclose à nouveau le boîte de dialogue hello.
5. toomake une transaction de sauvegarde du journal de base de données hello, **l’Explorateur d’objets**, développez **bases de données**, avec le bouton droit **MyDB1**, pointez trop**tâches**, puis cliquez sur **Back Up**.
6. Dans **Type de sauvegarde**, sélectionnez **Journal des transactions**. Conserver hello **Destination** fichier toohello de jeu de chemin d’accès un vous avez spécifié précédemment, puis cliquez sur **OK**. Une fois l’opération de sauvegarde hello se termine, cliquez sur **OK** à nouveau.
7. sauvegardes de journaux hello toorestore complète et transaction **ContosoSQL2**, ouvrez hello RDP du fichier pour **ContosoSQL2**, connectez-vous en tant que **CORP\Install**. Laisser une session Bureau à distance de hello pour **ContosoSQL1** ouvrir.
8. À partir de hello **Démarrer** menu, ouvrir **SQL Server Management Studio**, puis cliquez sur **Connect** instance de SQL Server tooconnect toohello par défaut.
9. Dans **l’Explorateur d’objets**, cliquez avec le bouton droit sur **Bases de données**, puis cliquez sur **Restaurer la base de données**.
10. Bonjour **Source** section, sélectionnez **périphérique**, puis cliquez sur les points de suspension hello **...** .
11. Dans **Sélectionner les unités de sauvegarde**, cliquez sur **Ajouter**.
12. Dans **Emplacement du fichier de sauvegarde**, saisissez **\\ContosoSQL1\backup**, cliquez sur **Actualiser**, sélectionnez **MyDB1.bak**, puis cliquez sur **OK** et de nouveau sur **OK**. Vous devez maintenant voir hello sauvegarde complète et sauvegarde du journal hello dans hello **toorestore de jeux de sauvegarde** volet.
13. Accédez toohello **Options** page, sélectionnez **RESTORE WITH NORECOVERY** dans **état de récupération**, puis cliquez sur **OK** base de données toorestore hello. Après avoir hello restaurer l’opération terminée, cliquez sur **OK**.

### <a name="create-hello-availability-group"></a>Créer le groupe de disponibilité hello
1. Allez sauvegarder la session Bureau à distance de toohello de **ContosoSQL1**. Dans **l’Explorateur d’objets** dans SQL Server Management Studio, cliquez sur **haute disponibilité Always On**, puis cliquez sur **Assistant Nouveau groupe de disponibilité**, comme indiqué dans hello capture d’écran suivante.
   
    ![Démarrer l’Assistant Nouveau groupe de disponibilité](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. Sur hello **Introduction** , cliquez sur **suivant**. Sur hello **spécifier un nom de groupe de disponibilité** , tapez **AG1** dans **nom du groupe de disponibilité**, puis cliquez sur **suivant** à nouveau.
   
    ![Assistant Nouveau groupe de disponibilité, spécifier le nom du groupe de disponibilité](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. Sur hello **sélectionner les bases de données** , sélectionnez **MyDB1**, puis cliquez sur **suivant**. base de données Hello remplit les conditions préalables de hello pour un groupe de disponibilité car vous avez effectué au moins une sauvegarde complète sur le réplica principal de hello prévue.
   
    ![Assistant Nouveau groupe de disponibilité, sélectionner des bases de données](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. sur hello **spécifier les réplicas** , cliquez sur **ajouter un réplica**.
   
    ![Assistant Nouveau groupe de disponibilité, spécifier les réplicas](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. Bonjour **connecter tooServer** boîte de dialogue, tapez **ContosoSQL2** dans **nom du serveur**, puis cliquez sur **connexion**.
   
    ![Assistant Nouveau groupe de disponibilité, connexion tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. Retour sur hello **spécifier les réplicas** page, vous devez maintenant voir **ContosoSQL2** répertoriés dans **réplicas disponibles**. Configurer des réplicas de hello comme indiqué dans hello suivant capture d’écran. Quand vous avez terminé, cliquez sur **Suivant**.
   
    ![Assistant Nouveau groupe de disponibilité, spécifier les réplicas (Terminé)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. Sur hello **sélectionner la synchronisation initiale des données** , sélectionnez **joindre uniquement**, puis cliquez sur **suivant**. Vous avez déjà effectué la synchronisation des données manuellement lorsque vous avez effectué les sauvegardes complète et de transaction hello sur **ContosoSQL1** et les restaurer sur **ContosoSQL2**. Vous pouvez choisir pas tooperform hello les opérations de sauvegarde et de restauration sur votre base de données et sélectionnez à la place **complète** toolet hello Assistant Nouveau groupe de disponibilité effectue la synchronisation des données pour vous. Toutefois, nous vous déconseillons d’utiliser cette option pour les grandes bases de données de certaines entreprises.
   
    ![Assistant Nouveau groupe de disponibilité, Sélectionner la synchronisation initiale des données](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. Sur hello **Validation** , cliquez sur **suivant**. Cette page doit ressembler toohello similaire après la capture d’écran. Il est un avertissement pour la configuration de l’écouteur hello, car vous n’avez pas configuré un écouteur de groupe de disponibilité. Vous pouvez ignorer cet avertissement, étant donné que ce didacticiel ne configure pas d’écouteur. écouteur de hello tooconfigure après avoir terminé ce didacticiel, consultez la rubrique [configurer un écouteur d’équilibrage de charge interne pour les groupes de disponibilité AlwaysOn dans Azure](../classic/ps-sql-int-listener.md).
   
    ![Assistant Nouveau groupe de disponibilité, Validation](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. Sur hello **Résumé** , cliquez sur **Terminer**, puis patientez pendant que l’Assistant hello configure le nouveau groupe de disponibilité hello. Sur hello **progression** page, vous pouvez cliquer sur **plus de détails** tooview hello détaillées de progression. Une fois hello Assistant terminé, inspecter hello **résultats** page tooverify ce groupe de disponibilité hello est correctement créé, comme indiqué dans hello suivant capture d’écran, puis cliquez sur **fermer** tooexit hello Assistant.
   
    ![Assistant Nouveau groupe de disponibilité, Résultats](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. Dans **l’Explorateur d’objets**, développez **Haute disponibilité Always On**, puis **Groupes de disponibilité**. Vous devez maintenant voir le nouveau groupe de disponibilité hello dans ce conteneur. Cliquez avec le bouton droit sur **AG1 (principal)**, puis cliquez sur **Afficher le tableau de bord**.
    
     ![Afficher le tableau de bord du groupe de disponibilité](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. Votre **tableau de bord AlwaysOn** doit rechercher similaire toohello un Bonjour suivant capture d’écran. Vous pouvez voir les réplicas hello, le mode de basculement hello de chaque réplica et l’état de synchronisation hello.
    
     ![Tableau de bord du groupe de disponibilité](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. Trop de retour**le Gestionnaire de serveur**, cliquez sur **outils**, puis ouvrez **Gestionnaire du Cluster de basculement**.
13. Développez **Cluster1.corp.contoso.com**, puis **Services et applications**. Sélectionnez **rôles** et notez que hello **AG1** rôle du groupe de disponibilité a été créé. Notez que AG1 n’a pas une adresse IP par base de données auquel les clients peuvent se connecter toohello le groupe de disponibilité, car vous n’avez pas configuré un port d’écoute. Vous pouvez vous connecter directement toohello le nœud principal pour les opérations de lecture-écriture et le nœud secondaire de hello pour les requêtes en lecture seule.
    
     ![Groupe de disponibilité dans le Gestionnaire du cluster de basculement](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> N’essayez pas de toofail sur les groupes de disponibilité hello hello Gestionnaire du Cluster de basculement. Vous devez effectuer toutes les opérations de basculement à partir du **tableau de bord Always On** dans SQL Server Management Studio. Pour plus d’informations, consultez [Restrictions d’utilisation hello Gestionnaire du Cluster de basculement avec des groupes de disponibilité](https://msdn.microsoft.com/library/ff929171.aspx).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Vous avez correctement implémenté SQL Server Always On en créant un groupe de disponibilité dans Azure. tooconfigure un écouteur pour ce groupe de disponibilité, consultez [configurer un écouteur d’équilibrage de charge interne pour les groupes de disponibilité Always On dans Azure](../classic/ps-sql-int-listener.md).

Pour en savoir plus sur l’utilisation de SQL Server dans Azure, consultez [SQL Server sur Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

