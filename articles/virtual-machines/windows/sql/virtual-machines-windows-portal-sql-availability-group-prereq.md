---
title: "groupes d’aaaSQL disponibilité du serveur - machines virtuelles - conditions préalables | Documents Microsoft"
description: "Ce didacticiel montre comment regroupement des conditions préalables de hello tooconfigure permettant de garantir une disponibilité de SQL Server Always On sur machines virtuelles Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Conditions préalables de hello complète pour la création de groupes de disponibilité Always On sur des machines virtuelles

Ce didacticiel montre comment toocomplete hello les conditions requises pour créer un [SQL Server Always On le groupe de disponibilité sur des machines virtuelles (VM) Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md). Lorsque vous avez terminé la configuration requise de hello, vous avez un serveur témoin, deux machines virtuelles de serveur SQL et un contrôleur de domaine dans un seul groupe de ressources.

**Durée estimée**: il peut prendre quelques heures conditions préalables de toocomplete hello. La majeure partie de ce temps est consacré à la création de machines virtuelles.

Hello diagramme suivant illustre ce que vous créez dans le didacticiel de hello.

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>Consulter la documentation sur le groupe de disponibilité

Ce didacticiel suppose que vous avez des notions de base sur les groupes de disponibilité AlwaysOn SQL Server. Si vous n’êtes pas familiarisé avec cette technologie, consultez [Vue d’ensemble des groupes de disponibilité AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).


## <a name="create-an-azure-account"></a>Création d'un compte Azure
Vous avez besoin d’un compte Azure. Vous pouvez [ouvrir un compte Azure gratuit](/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de l’abonnement à Visual Studio](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
1. Connectez-vous à toohello [portail Azure](http://portal.azure.com).
2. Cliquez sur  **+**  toocreate un nouvel objet dans le portail de hello.

   ![Nouvel objet](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. Type **groupe de ressources** Bonjour **Marketplace** fenêtre de recherche.

   ![Groupe de ressources](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. Cliquez sur **Groupe de ressources**.
5. Cliquez sur **Créer**.
6. Sur hello **groupe de ressources** panneau, sous **nom de groupe de ressources**, tapez un nom pour le groupe de ressources hello. Par exemple, tapez **sql-ha-rg**.
7. Si vous avez plusieurs abonnements Azure, vérifiez que l’abonnement hello est hello abonnement Azure souhaité dans le groupe de disponibilité toocreate hello.
8. Sélectionnez un emplacement. emplacement de Hello est hello région Azure où vous souhaitez le groupe de disponibilité toocreate hello. Pour ce didacticiel, nous allons toobuild toutes les ressources dans un emplacement Azure.
9. Vérifiez que **toodashboard du code confidentiel** est activée. Ce paramètre facultatif place un raccourci pour le groupe de ressources hello sur hello tableau de bord de portail Azure.

   ![Groupe de ressources](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. Cliquez sur **créer** groupe de ressources toocreate hello.

Azure crée des groupe de ressources hello et codes confidentiels un groupe de ressources toohello raccourci dans le portail de hello.

## <a name="create-hello-network-and-subnets"></a>Créer des sous-réseaux et hello réseau
étape suivante de Hello est toocreate des réseaux hello et sous-réseaux dans le groupe de ressources Azure hello.

solution de Hello utilise un réseau virtuel avec deux sous-réseaux. Hello [vue d’ensemble du réseau virtuel](../../../virtual-network/virtual-networks-overview.md) fournit plus d’informations sur les réseaux dans Azure.

réseau virtuel de hello toocreate :

1. Bonjour portail Azure, dans votre groupe de ressources, cliquez sur **+ ajouter**. Ouvre Azure hello **tout** panneau.

   ![Nouvel élément](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. Recherchez **Réseau virtuel**.

     ![Rechercher un réseau virtuel](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. Cliquez sur **Réseau virtuel**.
4. Sur hello **réseau virtuel** panneau, cliquez sur hello **le Gestionnaire de ressources** modèle de déploiement, puis cliquez sur **créer**.

    Hello tableau suivant présente les paramètres hello pour le réseau virtuel de hello :

   | **Champ** | Valeur |
   | --- | --- |
   | **Nom** |autoHAVNET |
   | **Espace d’adressage** |10.33.0.0/24 |
   | **Nom du sous-réseau** |Admin |
   | **Plage d’adresses de sous-réseau** |10.33.0.0/29 |
   | **Abonnement** |Spécifiez un abonnement hello que vous avez l’intention de toouse. Le champ **Abonnement** est vide si vous n'avez qu'un seul abonnement. |
   | **Groupe de ressources** |Choisissez **utiliser l’existante** et choisissez le nom hello hello du groupe de ressources. |
   | **Emplacement** |Spécifiez hello emplacement Azure. |

   Votre plage d’adresses adresse espace et le sous-réseau peut être différente de la table de hello. En fonction de votre abonnement, le portail de hello suggère un espace d’adressage disponible et la plage d’adresses de sous-réseau correspondant. Si vous ne disposez pas d’un espace d’adressage suffisant, utilisez un autre abonnement.

   exemple Hello utilise hello nom du sous-réseau **Admin**. Ce sous-réseau est hello des contrôleurs de domaine.

5. Cliquez sur **Créer**.

   ![Configurer un réseau virtuel hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure vous renvoie un tableau de bord de portail toohello et vous avertit lorsque le réseau de nouveau hello est créé.

### <a name="create-a-second-subnet"></a>Créer un deuxième sous-réseau
Hello nouveau réseau virtuel a un sous-réseau, nommé **Admin**. les contrôleurs de domaine hello utilisent ce sous-réseau. Hello machines virtuelles SQL Server utilisent un deuxième sous-réseau nommé **SQL**. tooconfigure ce sous-réseau :

1. Sur votre tableau de bord, cliquez sur le groupe de ressources hello que vous avez créé, **SQL-HA-RG**. Recherchez le réseau de hello dans le groupe de ressources hello sous **ressources**.

    Si **SQL-HA-RG** n’est pas visible, cliquez **groupes de ressources** et le filtrage par nom de groupe de ressources hello.
2. Cliquez sur **autoHAVNET** sur liste hello des ressources. Azure ouvre le panneau de configuration de réseau hello.
3. Sur hello **autoHAVNET** Panneau de réseau virtuel, sous **paramètres** , cliquez sur **sous-réseaux**.

    Notez le sous-réseau hello que vous avez déjà créé.

   ![Configurer un réseau virtuel hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. Créez un deuxième sous-réseau. Cliquez sur **+ Sous-réseau**.
6. Sur hello **ajouter un sous-réseau** panneau, configurez le sous-réseau de hello en tapant **sqlsubnet** sous **nom**. Azure spécifie automatiquement une **plage d’adresses**valide. Vérifiez que cette plage d’adresses comporte au moins 10 adresses. Dans un environnement de production, vous pouvez avoir besoin de davantage d’adresses.
7. Cliquez sur **OK**.

    ![Configurer un réseau virtuel hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

Hello tableau suivant résume les paramètres de configuration réseau hello :

| **Champ** | Valeur |
| --- | --- |
| **Nom** |**autoHAVNET** |
| **Espace d’adressage** |Cette valeur dépend des espaces d’adressage disponible hello dans votre abonnement. 10.0.0.0/16 est une valeur courante. |
| **Nom du sous-réseau** |**admin** |
| **Plage d’adresses de sous-réseau** |Cette valeur dépend des plages d’adresses disponibles hello dans votre abonnement. 10.0.0.0/24 est une valeur courante. |
| **Nom du sous-réseau** |**sqlsubnet** |
| **Plage d’adresses de sous-réseau** |Cette valeur dépend des plages d’adresses disponibles hello dans votre abonnement. 10.0.1.0/24 est une valeur courante. |
| **Abonnement** |Spécifiez un abonnement hello que vous avez l’intention de toouse. |
| **Groupe de ressources** |**SQL-HA-RG** |
| **Emplacement** |Spécifiez hello même emplacement que vous avez choisi pour le groupe de ressources hello. |

## <a name="create-availability-sets"></a>Créer des groupes à haute disponibilité

Avant de créer des machines virtuelles, vous devez toocreate à haute disponibilité. Haute disponibilité réduire le temps mort de hello pour les événements de maintenance planifiée ou non. Un groupe à haute disponibilité Azure est un groupe de ressources logique qu’Azure place dans des domaines de mise à jour et d’erreur physiques. Un domaine d’erreur garantit que les membres de hello du groupe à haute disponibilité hello ont des ressources réseau et d’alimentation distinctes. Un domaine de mise à jour garantit que les membres du groupe à haute disponibilité hello ne sont pas arrêtés pour maintenance à hello même temps. Pour plus d’informations, consultez [gérer la disponibilité hello des machines virtuelles](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Vous avez besoin de deux groupes à haute disponibilité. Un est hello des contrôleurs de domaine. Hello est ensuite pour les machines virtuelles hello SQL Server.

toocreate une disponibilité définie, passez le groupe de ressources toohello et cliquez sur **ajouter**. Filtrer les résultats de hello en tapant **à haute disponibilité**. Cliquez sur **à haute disponibilité** dans hello des résultats, puis cliquez sur **créer**.

Configurez deux groupes à haute disponibilité selon les paramètres toohello Bonjour tableau suivant :

| **Champ** | Groupe à haute disponibilité du contrôleur de domaine | Groupe à haute disponibilité SQL Server |
| --- | --- | --- |
| **Name** |adavailabilityset |sqlavailabilityset |
| **Groupe de ressources** |SQL-HA-RG |SQL-HA-RG |
| **Domaines d'erreur** |3 |3 |
| **Domaines de mise à jour** |5 |3 |

Après avoir créé des groupes à haute disponibilité hello, retourner le groupe de ressources toohello Bonjour portail Azure.

## <a name="create-domain-controllers"></a>Création de contrôleurs de domaine
Une fois que vous avez créé le réseau de hello, des sous-réseaux, haute disponibilité et un équilibrage de charge connecté à Internet, vous êtes prêt toocreate hello virtual machines hello des contrôleurs de domaine.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Créer des machines virtuelles hello contrôleurs de domaine
toocreate et configurez les contrôleurs de domaine hello, retourner toohello **SQL-HA-RG** groupe de ressources.

1. Cliquez sur **Add**. Hello **tout** panneau s’ouvre.
2. Tapez **Windows Server 2016 Datacenter**.
3. Cliquez sur **Windows Server 2016 Datacenter**. Bonjour **Windows Server 2016 Datacenter** panneau, vérifiez que ce modèle de déploiement hello est **le Gestionnaire de ressources**, puis cliquez sur **créer**. Ouvre Azure hello **créer la machine virtuelle** panneau.

Répétez hello précédentes étapes toocreate deux machines virtuelles. Nom hello deux des ordinateurs virtuels :

* ad-primary-dc
* ad-secondary-dc

  > [!NOTE]
  > Hello **ad-secondaire-dc** machine virtuelle est facultative, tooprovide haute disponibilité pour les Services de domaine Active Directory.
  >
  >

Hello tableau suivant présente les paramètres hello pour ces deux ordinateurs :

| **Champ** | Valeur |
| --- | --- |
| **Nom** |Premier contrôleur de domaine : *ad-primary-dc*.</br>Second contrôleur de domaine *ad-secondary-dc*. |
| **Type de disque de machine virtuelle** |SSD |
| **Nom d'utilisateur** |DomainAdmin |
| **Mot de passe** |Contoso!0000 |
| **Abonnement** |*Votre abonnement* |
| **Groupe de ressources** |SQL-HA-RG |
| **Emplacement** |*Votre emplacement* |
| **Taille** |DS1_V2 |
| **Stockage** | **Utiliser des disques gérés** - **Oui** |
| **Réseau virtuel** |autoHAVNET |
| **Sous-réseau** |admin |
| **Adresse IP publique** |*Identique à celui hello machine virtuelle* |
| **Groupe de sécurité réseau** |*Identique à celui hello machine virtuelle* |
| **Groupe à haute disponibilité** |adavailabilityset </br>**Domaines d'erreur** : 2</br>**Domaines de mise à jour** : 2|
| **Diagnostics** |Activé |
| **Compte de stockage de diagnostics** |*Créé automatiquement* |

   >[!IMPORTANT]
   >Vous pouvez uniquement placer une machine virtuelle dans un groupe de disponibilité lors de sa création. Vous ne pouvez pas modifier hello groupe à haute disponibilité après avoir créé une machine virtuelle. Consultez [gérer la disponibilité hello des machines virtuelles](../manage-availability.md).

Azure crée des machines virtuelles de hello.

Après avoir créé des machines virtuelles de hello, configurer le contrôleur de domaine hello.

### <a name="configure-hello-domain-controller"></a>Configurer le contrôleur de domaine hello
Bonjour, comme suit, configurer hello **ad-primary-dc** machine en tant que contrôleur de domaine pour corp.contoso.com.

1. Dans le portail de hello, ouvrez hello **SQL-HA-RG** groupe de ressources et sélectionnez hello **ad-primary-dc** machine. Sur hello **ad-primary-dc** panneau, cliquez sur **Connect** tooopen un RDP du fichier pour l’accès Bureau à distance.

    ![Connecter l’ordinateur virtuel de tooa](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. Connectez-vous avec votre compte Administrateur configuré (**\DomainAdmin**) et votre mot de passe (**Contoso!0000**).
3. Par défaut, hello **le Gestionnaire de serveur** tableau de bord doit être affiché.
4. Cliquez sur hello **ajouter des rôles et fonctionnalités** lien sur le tableau de bord hello.

    ![Gestionnaire de serveur - Ajouter des rôles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. Sélectionnez **suivant** jusqu'à ce que vous atteigniez toohello **rôles serveur** section.
6. Sélectionnez hello **les Services de domaine Active Directory** et **serveur DNS** rôles. Lorsque vous y êtes invité, ajoutez les fonctionnalités supplémentaires requises par ces rôles.

   > [!NOTE]
   > Windows vous avertit qu’il n’y a aucune adresse IP statique. Si vous testez la configuration de hello, cliquez sur **continuer**. Pour les scénarios de production, définissez hello IP adresse toostatic Bonjour portail Azure, ou [utiliser PowerShell tooset hello adresse IP de l’ordinateur du contrôleur de domaine hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   >
   >

    ![Boîte de dialogue Ajouter des rôles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. Cliquez sur **suivant** jusqu'à ce que vous atteigniez hello **Confirmation** section. Sélectionnez hello **redémarrez le serveur de destination hello automatiquement si nécessaire** case à cocher.
8. Cliquez sur **Installer**.
9. Une fois les fonctionnalités hello lors de l’installation, retournez toohello **le Gestionnaire de serveur** tableau de bord.
10. Sélectionnez hello nouvelle **AD DS** option dans le volet gauche de hello.
11. Cliquez sur hello **plus** lien dans la barre d’avertissement jaune de hello.

    ![Boîte de dialogue AD DS sur hello machine virtuelle du serveur DNS](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. Bonjour **Action** colonne Hello **tous les détails de la tâche serveur** boîte de dialogue, cliquez sur **promouvoir ce serveur de contrôleur de domaine tooa**.
13. Bonjour **Assistant Configuration de Services de domaine Active Directory**, utilisez hello valeurs suivantes :

    | **Page** | Paramètre |
    | --- | --- |
    | **Configuration du déploiement** |**Ajouter une nouvelle forêt**<br/> **Nom de domaine racine** = corp.contoso.com |
    | **Options de contrôleur de domaine :** |**Mot de passe DSRM** = Contoso!0000<br/>**Confirmer le mot de passe** = Contoso!0000 |
14. Cliquez sur **suivant** toogo via hello autres pages de l’Assistant de hello. Sur hello **vérification** , vérifiez que vous consultez hello message suivant : **toutes les vérifications des conditions préalables a réussi**. Vous pouvez passer en revue les messages d’avertissement applicables, mais il est possible de toocontinue avec l’installation de hello.
15. Cliquez sur **Installer**. Hello **ad-primary-dc** ordinateur virtuel redémarre automatiquement.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Notez l’adresse IP de hello hello principal du contrôleur de domaine

Utilisez le contrôleur de domaine principal hello de DNS. Notez l’adresse IP de contrôleur de domaine principal hello.

Adresse IP du contrôleur de domaine principal tooget monodirectionnelle hello est via hello portail Azure.

1. Sur hello portail Azure, ouvrez le groupe de ressources hello.

2. Cliquez sur le contrôleur de domaine principal hello.

3. Dans le panneau de contrôleur de domaine principal hello, cliquez sur **interfaces réseau**.

![Interfaces réseau](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

Notez l’adresse IP privée de hello pour ce serveur.

### <a name="configure-hello-virtual-network-dns"></a>Configurer le DNS du réseau virtuel hello
Une fois que vous créez le premier contrôleur de domaine hello et activez DNS sur le premier serveur de hello, configurez toouse de réseau virtuel hello ce serveur DNS.

1. Bonjour portail Azure, cliquez sur le réseau virtuel de hello.

2. Sous **Paramètres**, cliquez sur **Serveur DNS**.

3. Cliquez sur **personnalisé**et tapez Bonjour adresse IP privée du contrôleur de domaine principal hello.

4. Cliquez sur **Enregistrer**.

### <a name="configure-hello-second-domain-controller"></a>Configurer le contrôleur de domaine de deuxième hello
Après le redémarrage du contrôleur de domaine principal hello, vous pouvez configurer le deuxième contrôleur de domaine hello. Cette étape facultative intervient pour les scénarios de haute disponibilité. Suivez ces étapes tooconfigure hello second contrôleur de domaine :

1. Dans le portail de hello, ouvrez hello **SQL-HA-RG** groupe de ressources et sélectionnez hello **ad-secondaire-dc** machine. Sur hello **ad-secondaire-dc** panneau, cliquez sur **Connect** tooopen un RDP du fichier pour l’accès Bureau à distance.
2. Connectez-vous à toohello machine virtuelle à l’aide de votre compte d’administrateur configuré (**BUILTIN\DomainAdmin**) et le mot de passe (**Contoso ! 0000**).
3. Modification hello préféré adresse toohello adresse du serveur DNS du contrôleur de domaine hello.
4. Dans **Centre réseau et partage**, cliquez sur l’interface réseau hello.
   ![Interface réseau](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. Cliquez sur **Propriétés**.
6. Cliquez sur **Internet Protocol Version 4 (TCP/IPv4)**, puis sur **Propriétés**.
7. Sélectionnez **hello utilisation suivant des adresses de serveur DNS** et spécifiez l’adresse hello du contrôleur de domaine principal hello dans **serveur DNS préféré**.
8. Cliquez sur **OK**, puis **fermer** modifications de hello toocommit. Vous êtes maintenant en mesure de toojoin hello VM trop**corp.contoso.com**.

   >[!IMPORTANT]
   >Si vous perdez le Bureau à distance de hello connexion tooyour après avoir modifié le paramètre de DNS hello, accédez à toohello portal et redémarrez hello machine virtuelle Azure.

9. À partir du contrôleur de domaine secondaire hello toohello Bureau à distance, ouvrez **tableau de bord Gestionnaire de serveur**.
10. Cliquez sur hello **ajouter des rôles et fonctionnalités** lien sur le tableau de bord hello.

    ![Gestionnaire de serveur - Ajouter des rôles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. Sélectionnez **suivant** jusqu'à ce que vous atteigniez toohello **rôles serveur** section.
12. Sélectionnez hello **les Services de domaine Active Directory** et **serveur DNS** rôles. Lorsque vous y êtes invité, ajoutez les fonctionnalités supplémentaires requises par ces rôles.
13. Une fois les fonctionnalités hello lors de l’installation, retournez toohello **le Gestionnaire de serveur** tableau de bord.
14. Sélectionnez hello nouvelle **AD DS** option dans le volet gauche de hello.
15. Cliquez sur hello **plus** lien dans la barre d’avertissement jaune de hello.
16. Bonjour **Action** colonne Hello **tous les détails de la tâche serveur** boîte de dialogue, cliquez sur **promouvoir ce serveur de contrôleur de domaine tooa**.
17. Sous **Configuration de déploiement**, sélectionnez **ajouter un domaine existant de tooan de contrôleur de domaine**.
   ![Configuration du déploiement](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. Cliquez sur **Sélectionner**.
19. Se connecter à l’aide du compte d’administrateur hello (**CORP. Contoso.COM\domainadmin**) et le mot de passe (**Contoso ! 0000**).
20. Dans **sélectionnez un domaine dans la forêt de hello**et cliquez sur votre domaine, puis cliquez sur **OK**.
21. Dans **Options du contrôleur de domaine**, utilisez les valeurs par défaut de hello et définir un mot de passe DSRM.

   >[!NOTE]
   >Hello **Options DNS** page peut vous avertir qu’une délégation pour ce serveur DNS ne peut pas être créée. Vous pouvez ignorer cet avertissement dans les environnements hors production.
22. Cliquez sur **suivant** jusqu'à ce que la boîte de dialogue hello atteint hello **conditions préalables** vérifier. Cliquez ensuite sur **Installer**.

Après avoir hello serveur termine hello de modifications de configuration, redémarrez le serveur hello.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Ajouter hello toohello de contrôleur de domaine deuxième adresse IP privée toohello VPN DNS Server

Bonjour portail Azure, sous réseau virtuel, modifiez hello DNS tooinclude hello adresse IP du serveur de contrôleur de domaine secondaire hello. Cela permet la redondance des services DNS hello.

### <a name=DomainAccounts></a>Configurer des comptes de domaine hello

Dans les étapes suivantes hello, vous configurez hello les comptes Active Directory. Hello tableau suivant répertorie les comptes hello :

| |Compte d’installation<br/> |sqlserver-0 <br/>SQL Server et compte SQL Agent Service |sqlserver-1<br/>SQL Server et compte SQL Agent Service
| --- | --- | --- | ---
|**Prénom** |Installer |SQLSvc1 | SQLSvc2
|**SamAccountName de l'utilisateur** |Installer |SQLSvc1 | SQLSvc2

Utilisez hello suivant les étapes toocreate chaque compte.

1. Connectez-vous à toohello **ad-primary-dc** machine.
2. Dans **Gestionnaire de serveur**, sélectionnez **Outils**, puis cliquez sur **Centre d’administration Active Directory**.   
3. Sélectionnez **corp (local)** hello volet de gauche.
4. Sur la droite de hello **tâches** volet, sélectionnez **nouveau**, puis cliquez sur **utilisateur**.
   ![Centre d'administration Active Directory](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >Définissez un mot de passe complexe pour chaque compte.<br/> Pour les environnements de test, ensemble hello utilisateur compte toonever expirer.

5. Cliquez sur **OK** utilisateur de hello toocreate.
6. Répétez hello étapes précédentes pour chacun des trois comptes d’hello.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Accorder des autorisations de hello requis toohello compte d’installation
1. Bonjour **centre d’administration Active Directory**, sélectionnez **corp (local)** dans le volet gauche de hello. Puis Bonjour droite **tâches** volet, cliquez sur **propriétés**.

    ![Propriétés de l’utilisateur CORP](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. Sélectionnez **Extensions**, puis cliquez sur hello **avancé** bouton sur hello **sécurité** onglet.
3. Bonjour **des paramètres de sécurité avancés pour corp** boîte de dialogue, cliquez sur **ajouter**.
4. Cliquez sur **Sélectionnez un principal**, recherchez **CORP\Install**, puis cliquez sur **OK**.
5. Sélectionnez hello **lire toutes les propriétés** case à cocher.

6. Sélectionnez hello **Créer objets ordinateur** case à cocher.

     ![Autorisations de l’utilisateur Corp](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. Cliquez sur **OK**, puis sur **OK** à nouveau. Fermer hello **corp** fenêtre Propriétés.

Maintenant que vous avez terminé de configurer Active Directory et les objets utilisateur hello, créez deux machines virtuelles de serveur SQL et un machine virtuelle du serveur témoin. Joint ensuite tous les trois de domaine toohello.

## <a name="create-sql-server-vms"></a>Créer des machines virtuelles SQL Server

Créez trois machines virtuelles supplémentaires. solution de Hello requiert deux machines virtuelles avec des instances de SQL Server. Une troisième machine virtuelle fonctionnera comme témoin. Windows Server 2016 peut utiliser un [cloud témoin](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness), toutefois, pour la cohérence avec les systèmes d’exploitation précédents, ce document utilise une machine virtuelle pour témoin.  

Envisagez de hello suivant deisign décisions avant de continuer.

* **Stockage - Disques gérés Azure**

   Pour le stockage d’ordinateur virtuel hello, utilisez des disques gérés Azure. Microsoft recommande des machines virtuelles Managed Disks pour SQL Server. Géré gère le stockage des disques coulisses hello. En outre, lorsque les ordinateurs virtuels avec des disques gérés sont hello même ensemble de disponibilité, Azure distribue hello ressources tooprovide approprié une redondance de stockage. Pour plus d’informations, voir la page [Azure Managed Disks overview](../managed-disks-overview.md) (Vue d’ensemble d’Azure Managed Disks). Pour plus de détails sur les disques gérés dans un groupe à haute disponibilité, consultez [Utilisation de disques gérés pour les machines virtuelles dans le groupe à haute disponibilité](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).

* **Réseau - Adresses IP privées en production**

   Pour les ordinateurs virtuels de hello, ce didacticiel utilise des adresses IP publiques. Cela permet une connexion à distance directement de l’ordinateur virtuel de toohello sur hello internet - facilite les étapes de configuration. Dans les environnements de production, Microsoft recommande uniquement des adresses IP privées dans la commande tooreduce hello vulnérabilité l’encombrement d’instance de SQL Server hello ressource d’ordinateur virtuel.

### <a name="create-and-configure-hello-sql-server-vms"></a>Créer et configurer des machines virtuelles hello SQL Server
Créez ensuite trois machines virtuelles : deux machines virtuelles SQL Server et une machine virtuelle pour un nœud de cluster supplémentaire. toocreate de machines virtuelles hello, revenez en arrière toohello **SQL-HA-RG** groupe de ressources, cliquez sur **ajouter**, recherche hello approprié élément de la galerie, cliquez sur **Machine virtuelle**, puis Cliquez sur **à partir de la galerie**. Utilisez les informations de hello Bonjour suivant toohelp table vous créez des machines virtuelles de hello :


| Page | MV1 | MV2 | MV3 |
| --- | --- | --- | --- |
| Sélectionnez hello appropriée de la galerie |**Windows Server 2016 Datacenter** |**SQL Server 2016 SP1 Enterprise sur Windows Server 2016** |**SQL Server 2016 SP1 Enterprise sur Windows Server 2016** |
| **Notions** |**Nom** = cluster-fsw<br/>**Nom d’utilisateur** = DomainAdmin<br/>**Mot de passe** = Contoso!0000<br/>**Abonnement** = votre abonnement<br/>**Groupe de ressources** = SQL-HA-RG<br/>**Emplacement** = Votre emplacement Azure |**Nom** = sqlserver-0<br/>**Nom d’utilisateur** = DomainAdmin<br/>**Mot de passe** = Contoso!0000<br/>**Abonnement** = votre abonnement<br/>**Groupe de ressources** = SQL-HA-RG<br/>**Emplacement** = Votre emplacement Azure |**Nom** = sqlserver-1<br/>**Nom d’utilisateur** = DomainAdmin<br/>**Mot de passe** = Contoso!0000<br/>**Abonnement** = votre abonnement<br/>**Groupe de ressources** = SQL-HA-RG<br/>**Emplacement** = Votre emplacement Azure |
| Configuration de la machine virtuelle - **Taille** |**TAILLE** = DS1\_V2 (1 cœur, 3,5 Go) |**TAILLE** = DS2\_V2 (2 cœurs, 7 Go)</br>taille de Hello doit prendre en charge le stockage SSD (prise en charge des disques Premium. )) |**TAILLE** = DS2\_V2 (2 cœurs, 7 Go) |
| Configuration de la machine virtuelle - **Paramètres** |**Stockage** : Utiliser des disques gérés.<br/>**Réseau virtuel** = autoHAVNET<br/>**Sous-réseau** = sqlsubnet(10.1.1.0/24)<br/>**Adresse IP publique** générée automatiquement.<br/>**Groupe de sécurité réseau** = aucun<br/>**Diagnostics de surveillance** = activés<br/>**Compte de stockage de diagnostics** = utilisez un compte de stockage généré automatiquement<br/>**Groupe à haute disponibilité** = sqlAvailabilitySet<br/> |**Stockage** : Utiliser des disques gérés.<br/>**Réseau virtuel** = autoHAVNET<br/>**Sous-réseau** = sqlsubnet(10.1.1.0/24)<br/>**Adresse IP publique** générée automatiquement.<br/>**Groupe de sécurité réseau** = aucun<br/>**Diagnostics de surveillance** = activés<br/>**Compte de stockage de diagnostics** = utilisez un compte de stockage généré automatiquement<br/>**Groupe à haute disponibilité** = sqlAvailabilitySet<br/> |**Stockage** : Utiliser des disques gérés.<br/>**Réseau virtuel** = autoHAVNET<br/>**Sous-réseau** = sqlsubnet(10.1.1.0/24)<br/>**Adresse IP publique** générée automatiquement.<br/>**Groupe de sécurité réseau** = aucun<br/>**Diagnostics de surveillance** = activés<br/>**Compte de stockage de diagnostics** = utilisez un compte de stockage généré automatiquement<br/>**Groupe à haute disponibilité** = sqlAvailabilitySet<br/> |
| Configuration de la machine virtuelle - **Paramètres SQL Server** |Non applicable |**Connectivité SQL** = privée (dans le réseau virtuel)<br/>**Port** = 1433<br/>**Authentification SQL** = désactivée<br/>**Configuration du stockage** = général<br/>**Mise à jour corrective automatisée** : dimanche à 2h00<br/>**Sauvegarde automatisée** = désactivée</br>**Intégration Azure Key Vault** = Désactivée |**Connectivité SQL** = privée (dans le réseau virtuel)<br/>**Port** = 1433<br/>**Authentification SQL** = désactivée<br/>**Configuration du stockage** = général<br/>**Mise à jour corrective automatisée** : dimanche à 2h00<br/>**Sauvegarde automatisée** = désactivée</br>**Intégration Azure Key Vault** = Désactivée |

<br/>

> [!NOTE]
> tailles de machine Hello suggérées ici sont destinées aux groupes de disponibilité de test dans des machines virtuelles Azure. Pour des performances optimales hello sur les charges de production, voir les recommandations de hello pour les tailles d’ordinateur SQL Server et la configuration dans [performances meilleures pratiques pour SQL Server dans des machines virtuelles](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

Une fois que les machines virtuelles de hello trois sont totalement configurées, vous devez toojoin les toohello **corp.contoso.com** domaine et allocation de machines toohello à CORP\Install des droits d’administration.

### <a name="joinDomain"></a>Joindre hello serveurs toohello domaine

Vous êtes maintenant en mesure de toojoin hello des machines virtuelles trop**corp.contoso.com**. Suit hello pour les machines virtuelles hello SQL Server et le fichier de hello partage le serveur témoin :

1. Se connecter à distance de machine virtuelle toohello **BUILTIN\DomainAdmin**.
2. Dans le **Gestionnaire de serveur**, cliquez sur **Serveur Local**.
3. Cliquez sur hello **groupe de travail** lien.
4. Bonjour **nom de l’ordinateur** , cliquez sur **modification**.
5. Sélectionnez hello **domaine** et tapez **corp.contoso.com** dans la zone de texte hello. Cliquez sur **OK**.
6. Bonjour **sécurité Windows** boîte de dialogue contextuelle, spécifiez les informations d’identification hello pour le compte d’administrateur par défaut hello (**CORP\DomainAdmin**) et le mot de passe hello (**Contoso ! 0000**).
7. Lorsque vous voyez le message de salutation « domaine corp.contoso.com de bienvenue toohello », cliquez sur **OK**.
8. Cliquez sur **fermer**, puis cliquez sur **redémarrer maintenant** dans la boîte de dialogue contextuelle hello.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>Ajouter un utilisateur de Corp\Install hello en tant qu’administrateur sur chaque ordinateur virtuel de cluster

Après le redémarrage de chaque ordinateur virtuel en tant que membre du domaine de hello, ajoutez **CORP\Install** en tant que membre du groupe Administrateurs local de hello.

1. Attendez que hello machine virtuelle est redémarré, puis lancez le fichier RDP de hello à partir de toosign de contrôleur de domaine principal hello dans trop**sqlserver-0** à l’aide de hello **CORP\DomainAdmin** compte.
   >[!TIP]
   >Veillez à vous connecter avec un compte d’administrateur de domaine de hello. Dans les étapes précédentes hello, vous utilisiez un compte d’administrateur intégré dans hello. Maintenant que hello serveur est dans le domaine de hello, utiliser le compte de domaine de hello. Dans votre session RDP, spécifiez *DOMAINE*\\*nom d’utilisateur*.

2. Dans **Gestionnaire de serveur**, sélectionnez **Outils**, puis cliquez sur **Gestion de l’ordinateur**.
3. Bonjour **gestion de l’ordinateur** fenêtre, développez **utilisateurs et groupes locaux**, puis sélectionnez **groupes**.
4. Double-cliquez sur hello **administrateurs** groupe.
5. Bonjour **propriétés du groupe Administrateurs** boîte de dialogue, cliquez sur hello **ajouter** bouton.
6. Entrez hello utilisateur **CORP\Install**, puis cliquez sur **OK**.
7. Cliquez sur **OK** tooclose hello **propriétés de l’administrateur** boîte de dialogue.
8. Répétez les étapes précédentes hello sur **sqlserver-1** et **fsw de cluster**.

### <a name="setServiceAccount"></a>Définir des comptes de service SQL Server hello

Sur chaque machine virtuelle SQL Server, définissez le compte de service SQL Server hello. Utiliser des comptes hello que vous avez créé lorsque vous [configuré des comptes de domaine hello](#DomainAccounts).

1. Ouvrez le **Gestionnaire de configuration de SQL Server**.
2. Service de SQL Server hello d’avec le bouton droit, puis cliquez sur **propriétés**.
3. Définir le compte hello et le mot de passe.
4. Répétez ces étapes sur hello autre machine virtuelle SQL Server.  

Pour les groupes de disponibilité de SQL Server, chaque machine virtuelle SQL Server doit toorun comme compte de domaine.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Créer une connexion dans sur chaque machine virtuelle SQL Server pour le compte d’installation Bonjour

Utilisez le groupe de disponibilité du compte (CORP\install) tooconfigure hello hello installation. Ce compte doit toobe membre hello **sysadmin** rôle serveur fixe sur chaque machine virtuelle SQL Server. Hello étapes suivantes créent une connexion dans hello du compte d’installation :

1. Se connecter toohello server via hello protocole RDP (Remote Desktop) à l’aide de hello  *\<MachineName\>\DomainAdmin* compte.

1. Ouvrez SQL Server Management Studio et connectez-vous toohello instance locale de SQL Server.

1. Dans l'**Explorateur d’objets**, cliquez sur **Sécurité**.

1. Cliquez avec le bouton droit sur **Connexions**. Cliquez sur **Nouvelle connexion**.

1. Dans **Nouvelle connexion**, cliquez sur **Rechercher**.

1. Cliquez sur **Emplacements**.

1. Entrez les informations d’identification de hello domaine administrateur réseau.

1. Utilisez le compte d’installation hello.

1. Définir hello connectez-vous toobe membre hello **sysadmin** rôle serveur fixe.

1. Cliquez sur **OK**.

Répétez hello précédentes étapes sur hello autre machine virtuelle SQL Server.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>Ajouter le Clustering de basculement tooboth de fonctionnalités machines virtuelles SQL Server

fonctionnalités de Clustering de basculement tooadd, hello suivant sur les deux machines virtuelles SQL Server :

1. Connexion de machine virtuelle de SQL Server toohello via hello protocole RDP (Remote Desktop) à l’aide de hello *CORP\install* compte. Ouvrez le **Tableau de bord de gestionnaire de serveur**.
2. Cliquez sur hello **ajouter des rôles et fonctionnalités** lien sur le tableau de bord hello.

    ![Gestionnaire de serveur - Ajouter des rôles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. Sélectionnez **suivant** jusqu'à ce que vous atteigniez toohello **fonctionnalités Server** section.
4. Dans **Fonctionnalités**, sélectionnez **Clustering de basculement**.
5. Ajoutez les fonctionnalités supplémentaires requises.
6. Cliquez sur **installer** fonctionnalités de hello tooadd.

Répétez les étapes hello sur hello autre machine virtuelle SQL Server.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">Configurer le pare-feu de hello sur chaque machine virtuelle SQL Server

solution de Hello nécessite hello suivant des ports TCP toobe ouvrir dans le pare-feu hello :

- **Machine virtuelle SQL Server** :<br/>
   le port 1433 pour une instance SQL Server par défaut.
- **Sonde Azure Load Balancer :**<br/>
   N’importe quel port disponible. Les exemples utilisent souvent le port 59999.
- **Point de terminaison de mise en miroir de bases de données :** <br/>
   N’importe quel port disponible. Les exemples utilisent souvent le port 5022.

Hello pare-feu ports besoin toobe est ouvert sur les deux machines virtuelles SQL Server.

méthode Hello ouverture des ports de hello dépend de la solution de pare-feu hello que vous utilisez. section suivante de Hello explique comment tooopen hello ports dans le pare-feu Windows. Ouvrez les ports hello requis sur chacun de vos machines virtuelles SQL Server.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Ouvrir un port TCP dans le pare-feu hello

1. Sur hello première SQL Server **Démarrer** écran, lancez **pare-feu Windows avec fonctions avancées de sécurité**.
2. Dans le volet gauche de hello, sélectionnez **règles de trafic entrant**. Dans le volet droit de hello, cliquez sur **nouvelle règle**.
3. Dans **Type de règle**, choisissez **Port**.
4. Pour le port de hello, spécifiez **TCP** et hello du type approprié de numéros de port. Consultez hello l’exemple suivant :

   ![Pare-feu SQL](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. Cliquez sur **Suivant**.
6. Sur hello **Action** page, conservez **autoriser la connexion hello** sélectionné, puis cliquez sur **suivant**.
7. Sur hello **profil** page, acceptez les paramètres par défaut de hello et puis cliquez sur **suivant**.
8. Sur hello **nom** , spécifiez un nom de règle (tel que **sonde d’équilibrage de charge Azure**) Bonjour **nom** zone de texte, puis cliquez sur **Terminer**.

Répétez ces étapes sur hello deuxième machine virtuelle de serveur SQL.

## <a name="next-steps"></a>Étapes suivantes

* [Créer un groupe de disponibilité AlwaysOn sur des machines virtuelles Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
