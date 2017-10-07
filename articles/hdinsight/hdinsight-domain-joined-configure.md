---
title: "les clusters appartenant à un domaine de HDInsight aaaConfigure - Azure | Documents Microsoft"
description: "Découvrez comment tooset installer et configurer des clusters HDInsight de domaine"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>Configurer des clusters HDInsight joints à un domaine (version préliminaire)

Découvrez comment tooset d’un Azure HDInsight cluster avec Azure Active Directory (Azure AD) et [Apache Ranger](http://hortonworks.com/apache/ranger/) tootake les avantages de l’authentification forte et politiques d’accès complet de basée sur les rôles (RBAC).  Le cluster HDInsight peut être configuré uniquement sur les clusters Linux. Pour plus d’informations, consultez [Introduire des clusters HDInsight joints à un domaine](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie n’est pas activé sur HDInsight joint à un domaine.

Cet article est le premier didacticiel de hello d’une série :

* Créer un tooAzure de cluster connecté HDInsight AD (via la fonctionnalité de Services de domaine Active Azure hello) avec Ranger Apache activée.
* Créer et appliquer des stratégies via Ranger d’Apache Hive et autoriser les utilisateurs (par exemple, les chercheurs de données) tooHive tooconnect à l’aide des outils basés sur ODBC, par exemple Excel, etc. de Tableau. Microsoft travaille sur l’ajout d’autres charges de travail, telles que HBase, Spark et Storm, appartenant à un tooDomain de HDInsight bientôt.

Un exemple de topologie finale de hello se présente comme suit :

![Topologie HDInsight jointe à un domaine](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Azure AD ne prenant en charge que les réseaux virtuels Classic et les clusters HDInsight Linux ne prenant en charge que les réseaux virtuels Azure Resource Manager, l’intégration HDInsight Azure AD requiert deux réseaux virtuels et une homologation mutuelle. Pour plus d’informations hello comparaison entre les modèles de déploiement hello deux, consultez [Azure Resource Manager et déploiement classique : comprendre les modèles de déploiement et état de vos ressources de hello](../azure-resource-manager/resource-manager-deployment-model.md). Hello deux réseaux virtuels doivent être Bonjour même région que hello Azure AD DS.

Les noms de service Azure doivent être globalement uniques. Hello suivant de noms est utilisé dans ce didacticiel. Contoso est un nom fictif. Vous devez remplacer *contoso* avec un nom différent lorsque vous parcourez le didacticiel de hello. 

**Noms :**

| Propriété | Valeur |
| --- | --- |
| Réseau virtuel Azure AD |contosoaadvnet |
| Groupe de ressources du réseau virtuel Azure AD |contosoaadrg |
| Annuaire Azure AD |contosoaaddirectory |
| Nom de domaine Azure AD |contoso (contoso.onmicrosoft.com) |
| Réseau virtuel HDInsight |contosohdivnet |
| Groupe de ressources du réseau virtuel HDInsight |contosohdirg |
| Cluster HDInsight |contosohdicluster |

Ce didacticiel fournit des étapes de hello pour la configuration d’un cluster HDInsight appartenant au domaine. Chaque section contient des articles tooother de liens avec plus d’informations.

## <a name="prerequisite"></a>Configuration requise :
* Familiarisez-vous avec les [services de domaine Azure AD](https://azure.microsoft.com/services/active-directory-ds/), et la structure de [tarification](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Assurez-vous que votre abonnement est dans la liste approuvée de cette version préliminaire publique. Vous pouvez le faire en envoyant un e-mail toohdipreview@microsoft.com avec votre ID d’abonnement.
* Un certificat SSL signé par une autorité signataire pour votre domaine. certificat de Hello est requise par la configuration de LDAP sécurisé. Les certificats auto-signés ne peuvent pas être utilisés.

## <a name="procedures"></a>Procédures
1. Créez un réseau virtuel Azure pour votre instance Azure AD.  
2. Créez et configurez Azure AD et Azure AD AS.
3. Créer un HDInsight VNet dans le mode de gestion des ressources Azure hello.
4. Homologue hello deux réseaux virtuels.
5. Créez un cluster HDInsight.

> [!NOTE]
> Ce didacticiel part du principe que vous ne possédez pas d’instance Azure AD. Si vous avez un, vous pouvez ignorer la partie hello à l’étape 2.
> 
> 

Il existe un script PowerShell qui automatise les étapes 3 à 7.  Pour plus d’informations, consultez la section [Configurer des clusters HDInsight joints à un domaine à l’aide d’Azure PowerShell](hdinsight-domain-joined-configure-use-powershell.md).

## <a name="create-an-azure-virtual-network-classic"></a>Création d'un réseau virtuel Azure (classique)
Dans cette section, vous créez un réseau virtuel (classique) à l’aide de hello portail Azure. Dans la section suivante de hello, vous activez hello Azure AD DS pour votre annuaire Azure AD dans le réseau virtuel de hello. Pour plus d’informations sur hello procédure et d’autres méthodes de création de réseau virtuel, consultez [créer un réseau virtuel (classique) à l’aide de hello Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

**toocreate un réseau virtuel classique**

1. Ouverture de session toohello [portail Azure](https://portal.azure.com). 
2. Cliquez sur **Nouveau** > **Mise en réseau** > **Réseau virtuel**.
3. Dans **Sélectionner un modèle de déploiement**, sélectionnez **Classique**, puis cliquez sur **Créer**.
4. Entrez ou sélectionnez hello valeurs suivantes :
   
   * **Nom** : contosoaadvnet
   * **Espace d’adressage** : 10.1.0.0/16
   * **Nom du sous-réseau** : Subnet1
   * **Plage d’adresses de sous-réseau** : 10.1.0.0/24
   * **Abonnement** : (sélectionnez un abonnement utilisé pour la création de ce réseau virtuel.)
   * **ResourceGroup** : contosoaadrg
   * **Emplacement** : (Sélectionnez une région pour votre cluster HDInsight.)
     
     > [!IMPORTANT]
     > Vous devez choisir un emplacement qui prend en charge Azure AD DS. Pour plus d’informations, consultez [Disponibilité des produits par région](https://azure.microsoft.com/en-us/regions/services/). 
     > 
     > Les deux hello réseau virtuel classique et hello réseau virtuel du groupe de ressources doit être hello même région que hello Azure AD DS.
     > 
     > 
5. Cliquez sur **créer** toocreate hello réseau virtuel.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Créez et configurer Azure AD AS pour votre instance Azure AD
Dans cette section, vous allez :

1. Créer une application Azure AD.
2. Créer des utilisateurs Azure AD. Ces utilisateurs sont des utilisateurs du domaine. Vous utilisez premier utilisateur de hello pour la configuration de cluster de HDInsight hello avec hello Azure AD.  Hello autres deux utilisateurs sont facultatifs pour ce didacticiel. Ils seront utilisés dans la section [Configuration de stratégies Hive pour les clusters HDInsight joints à un domaine](hdinsight-domain-joined-run-hive.md), au moment de la configuration des stratégies Apach Ranger.
3. Créer le groupe d’administrateurs du contrôleur de domaine AAD hello et ajouter un groupe de toohello utilisateur hello Azure AD. Vous utilisez cette unité d’organisation utilisateur toocreate hello.
4. Activer les Services de domaine Active Directory de Azure (Azure AD DS) pour hello Azure AD.
5. Configurer LDAPS pour hello Azure AD. Hello LDAP Lightweight Directory Access Protocol () est utilisé tooread à partir d’et écrire tooAzure AD.

Si vous préférez toouse une annonce Azure existant, vous pouvez ignorer les étapes 1 et 2.

**toocreate une annonce d’Azure**

1. À partir de hello [portail Azure classic](https://manage.windowsazure.com), cliquez sur **nouveau** > **des Services d’application** > **Active Directory**  >  **Active** > **création personnalisée**. 
2. Entrez ou sélectionnez hello valeurs suivantes :
   
   * **Nom** : contosoaaddirectory
   * **Nom de domaine** : contoso.  Ce nom doit être globalement unique.
   * **Pays ou région** : sélectionnez votre pays ou région.
3. Cliquez sur **Terminé**.

**Créer un utilisateur Azure AD**

1. À partir de hello [portail Azure classic](https://manage.windowsazure.com), cliquez sur **Active Directory** -> **contosoaaddirectory**. 
2. Cliquez sur **utilisateurs** à partir du menu du haut hello.
3. Cliquez sur **Add User**.
4. Saisissez **Nom d’utilisateur**, puis cliquez sur **Suivant**. 
5. Configurez le profil utilisateur ; dans **Rôle**, sélectionnez **Administrateur global**, puis cliquez sur **Suivant**.  rôle d’administrateur général Hello est toocreate nécessaires des unités d’organisation.
6. Cliquez sur **créer** tooget un mot de passe temporaire.
7. Effectuer une copie du mot de passe hello, puis cliquez sur **Complete**. Plus loin dans ce didacticiel, vous utiliserez ce cluster HDInsight hello de toocreate d’utilisateur administrateur global.

Suivez hello même procédure toocreate deux utilisateurs supplémentaires avec hello **utilisateur** rôle, hiveuser1 et hiveuser2. Hello utilisateurs suivants seront utilisées dans [configurer la ruche de stratégies pour les clusters HDInsight de joints au domaine](hdinsight-domain-joined-run-hive.md).

**toocreate hello du groupe Administrateurs du contrôleur de domaine AAD et ajouter un utilisateur Azure AD**

1. À partir de hello [portail Azure classic](https://manage.windowsazure.com), cliquez sur **Active Directory** > **contosoaaddirectory**. 
2. Cliquez sur **groupes** à partir du menu du haut hello.
3. Cliquez sur **Ajouter un groupe** ou **Ajouter groupe**.
4. Entrez ou sélectionnez hello valeurs suivantes :
   
   * **Nom** : AAD DC Administrators.  Ne pas de modifier le nom du groupe hello.
   * **Type de groupe** : Sécurité.
5. Cliquez sur **Terminé**.
6. Cliquez sur **administrateurs du contrôleur de domaine AAD** groupe de hello tooopen.
7. Cliquez sur **Ajouter des membres**.
8. Sélectionnez hello premier utilisateur créé à l’étape précédente de hello, puis cliquez sur **Complete**.
9. Répétition hello appelé d’un autre groupe même étapes toocreate **HiveUsers**, puis ajoutez hello deux ruche utilisateurs toohello groupe.

Pour plus d’informations, consultez [créer des Services de domaine Active Directory de Azure (aperçu) - hello 'Administrateurs du contrôleur de domaine AAD' groupe](../active-directory-domain-services/active-directory-ds-getting-started.md).

**tooenable Azure AD DS pour votre annuaire Azure AD**

1. À partir de hello [portail Azure classic](https://manage.windowsazure.com), cliquez sur **Active Directory** > **contosoaaddirectory**. 
2. Cliquez sur **configurer** à partir du menu du haut hello.
3. Faites défiler la liste trop**Services de domaine**, et ensemble hello des valeurs suivantes :
   
   * **Activer les services de domaine pour cet annuaire** : Oui.
   * **Nom de domaine DNS des services de domaine**: cela indique nom DNS hello Azure directory hello par défaut. Par exemple, contoso.onmicrosoft.com.
   * **Connecter le réseau virtuel de domaine services toothis**: sélectionnez hello classique réseau virtuel, vous avez créé précédemment, par exemple, **contosoaadvnet**.
4. Cliquez sur **enregistrer** bas hello de page de hello. Vous verrez **en attente...**  suivant trop**activer les services de domaine pour ce répertoire**.  
5. Attendez que l’indication **En attente ...** disparaisse et que le champ **Adresse IP** soit renseigné. Deux adresses IP sont renseignées. Il s’agit des adresses IP de hello hello des contrôleurs de domaine configurés par les Services de domaine. Chaque adresse IP sera visible une fois que le contrôleur de domaine hello correspondant est approvisionné et prêt. Notez que deux adresses IP de hello. Vous en aurez besoin ultérieurement.

)Pour plus d’informations, consultez [Services de domaine Azure AD (version préliminaire) - Activer Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).

**mot de passe toosynchronize**

Si vous utilisez votre propre domaine, vous avez besoin de mot de passe toosynchronize hello. Consultez [activer les services de domaine de mot de passe synchronisation tooAzure AD pour une Azure cloud uniquement annuaire AD](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).

**tooconfigure LDAPS pour hello Azure AD**

1. Récupérez un certificat SSL signé par une autorité signataire pour votre domaine. Si vous voulez toouse un certificat auto-signé, veuillez contacter toohdipreview@microsoft.com pour une exception.
2. À partir de hello [portail Azure classic](https://manage.windowsazure.com), cliquez sur **Active Directory** > **contosoaaddirectory**. 
3. Cliquez sur **configurer** à partir du menu du haut hello.
4. Faites défiler trop**services de domaine**.
5. Cliquez sur **Configurer le certificat**.
6. Suivez le fichier de certificat hello instruction toospecify hello et un mot de passe hello. Vous verrez **en attente...**  suivant trop**activer les services de domaine pour ce répertoire**.  
7. Attendez que l’indication **En attente...** disparaisse, puis que le champ **Certificat LDAP sécurisé** soit renseigné.  Cela peut prendre jusqu’à 10 minutes ou plus.

> [!NOTE]
> Si certaines tâches en arrière-plan sont en cours d’exécution sur hello Azure AD DS, vous pouvez voir une erreur lors du téléchargement du certificat - <i>est une opération en cours d’exécution pour ce client. Veuillez réessayer plus tard</i>.  Si vous rencontrez cette erreur, veuillez réessayer plus tard. Hello QU'IP du deuxième contrôleur de domaine peut prendre jusqu'à too3 heures toobe est configuré.
> 
> 

Pour plus d’informations, consultez [Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine géré par les services de domaine Azure AD](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>Créer un réseau virtuel Resource Manager pour le cluster HDInsight
Dans cette section, vous allez créer un VNet Gestionnaire de ressources Azure qui sera utilisé pour le cluster HDInsight de hello. Pour plus d’informations sur la création d’un réseau virtuel Azure à l’aide d’autres méthodes, consultez la section [Créez un réseau virtuel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

Après avoir créé le hello réseau virtuel, vous allez configurer hello toouse du Gestionnaire de ressources VNet hello mêmes serveurs DNS en tant que pour hello réseau virtuel de Azure AD. Si vous avez suivi les étapes de hello dans ce didacticiel toocreate hello classique de réseau virtuel et de hello Azure AD, les serveurs DNS hello sont 10.1.0.4 et 10.1.0.5.

**toocreate un VNet le Gestionnaire de ressources**

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau**, **Mise en réseau**, puis sur **Réseau virtuel**. 
3. Sous **Sélectionnez un modèle de déploiement**, sélectionnez **Resource Manager**, puis cliquez sur **Créer**.
4. Tapez ou sélectionnez hello valeurs suivantes :
   
   * **Nom** : contosohdivnet
   * **Espace d’adressage** : 10.2.0.0/16. Assurez-vous que la plage d’adresses hello ne peut pas chevaucher avec la plage d’adresses IP hello Hello réseau virtuel classique.
   * **Nom du sous-réseau** : Subnet1
   * **Plage d’adresses du sous-réseau** : 10.2.0.0/24
   * **Abonnement** : (sélectionnez votre abonnement Azure.)
   * **Groupe de ressources** : contosohdirg
   * **Emplacement**: (sélectionnez hello même emplacement que hello réseau virtuel de Azure AD, par exemple, contosoaadvnet).
5. Cliquez sur **Créer**.

**tooconfigure DNS pourquoi le Gestionnaire de ressources VNet**

1. À partir de hello [portail Azure](https://portal.azure.com), cliquez sur **davantage de services** -> **réseaux virtuels**. Vérifiez pas tooclick **des réseaux virtuels (classiques)**.
2. Cliquez sur **contosohdivnet**.
3. Cliquez sur **serveurs DNS** de hello gauche du Panneau de nouveau hello.
4. Cliquez sur **personnalisé**, puis entrez hello valeurs suivantes :
   
   * 10.1.0.4
   * 10.1.0.5
     
     Ces adresses IP du serveur DNS doivent correspondre à des serveurs DNS toohello hello réseau virtuel (VNet classique) de Azure AD.
5. Cliquez sur **Enregistrer**.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Homologue hello réseau virtuel de Azure AD et hello HDInsight VNet
**toopeer hello deux réseaux**

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **davantage de services** à partir du menu de gauche hello.
3. Cliquez sur **Réseaux virtuels**. Ne cliquez pas sur **Réseaux virtuels (classiques)**.
4. Cliquez sur **contosohdivnet**.  Il s’agit de hello HDInsight VNet.
5. Cliquez sur **homologations** sur le menu de gauche hello du Panneau de hello.
6. Cliquez sur **ajouter** à partir du menu du haut hello. Il ouvre hello **ajouter d’homologation** panneau.
7. Sur hello **ajouter d’homologation** panneau, définissez ou sélectionnez hello valeurs suivantes :
   
   * **Nom** : ContosoAADHDIVNetPeering
   * **Modèle de déploiement de réseau virtuel** : classique
   * **Abonnement**: sélectionnez votre nom d’abonnement utilisé pour le réseau virtuel de hello classique (Azure AD).
   * **Réseau virtuel** : contosoaadvnet.
   * **Autoriser l’accès au réseau virtuel** : (vérification)
   * **Autoriser le trafic transféré** : (vérification). Laissez hello autres deux cases à cocher est désactivée.
8. Cliquez sur **OK**.

## <a name="create-hdinsight-cluster"></a>Créer un cluster HDInsight
Dans cette section, vous créez un cluster basé sur Linux de Hadoop dans HDInsight à l’aide d’un portail Azure hello ou [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Pour d’autres méthodes de création de cluster et les paramètres de hello, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md). Pour plus d’informations sur l’utilisation du Gestionnaire de ressources du modèle toocreate Hadoop dans HDInsight les clusters, consultez [Hadoop de créer des clusters dans HDInsight à l’aide de modèles de gestionnaire de ressources](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**un cluster HDInsight de domaine à l’aide de toocreate hello portail Azure**

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau**, **Intelligence et analyse**, puis sur **HDInsight**.
3. À partir de hello **HDInsight nouveau cluster** panneau, entrez ou sélectionnez hello valeurs suivantes :
   
   * **Nom du cluster**: entrez un nouveau nom de cluster pour le cluster HDInsight de domaine de hello.
   * **Abonnement** : sélectionnez l’abonnement Azure utilisé pour créer ce cluster.
   * **Configuration du cluster** :
     
     * **Type de cluster** : Hadoop Actuellement, le cluster HDInsight joint au domaine est uniquement pris en charge sur les clusters Hadoop.
     * **Système d’exploitation** : Linux  Le cluster HDInsight joint au domaine est pris en charge uniquement sur les clusters HDInsight Linux.
     * **Version** : HDI 3.6. HDInsight joint au domaine est pris en charge uniquement sur le cluster HDInsight version 3.6.
     * **Type de cluster** : PREMIUM
       
       Cliquez sur **sélectionnez** modifications de hello toosave.
   * **Informations d’identification**: hello informations d’identification utilisateur de cluster hello et utilisateur SSH hello.
   * **Source de données**: créer un nouveau compte de stockage ou utiliser un compte de stockage existant comme compte de stockage par défaut pour le cluster HDInsight de hello de hello. emplacement de Hello doit être hello identique hello deux réseaux virtuels.  emplacement de Hello est également hello du cluster HDInsight de hello.
   * **Tarification**: sélectionnez nombre hello de nœuds de travail de votre cluster.
   * **Configurations avancées** : 
     
     * **Jonction de domaine et réseau virtuel/sous-réseau** : 
       
       * **Paramètres du domaine** : 
         
         * **Nom du domaine** : contoso.onmicrosoft.com
         * **Mot de passe utilisateur du domaine** :saisissez un nom d’utilisateur du domaine. Ce domaine doit avoir hello suivant des privilèges : joindre machines toohello domaine et les placer dans l’unité d’organisation hello vous spécifiez lors de la création du cluster ; Créer des principaux de service au sein de l’unité d’organisation hello que vous spécifiez lors de la création du cluster ; Créer des entrées DNS inverses. Cet utilisateur de domaine devient administrateur hello de ce cluster HDInsight appartenant au domaine.
         * **Mot de passe de domaine**: entrez le mot de passe utilisateur de domaine hello.
         * **Unité d’organisation**: entrez hello le nom unique de hello unité d’organisation que vous souhaitez toouse avec le cluster HDInsight. Par exemple : UO = HDInsightOU, CD = contoso, CD = onmicrosoft, CD = com. Si cette unité d’organisation n’existe pas, cluster HDInsight tentera toocreate cette unité d’organisation. Vérifiez que hello unité d’organisation existe déjà ou compte de domaine de hello dispose des autorisations toocreate un nouveau. Si vous utilisez le compte de domaine hello qui fait partie du groupe Administrateurs de AADDC, il aura des autorisations nécessaires toocreate hello unité d’organisation.
         * **URL LDAPS** : ldaps://contoso.onmicrosoft.com:636
         * **Groupe d’utilisateurs accès**: spécifiez de groupe de sécurité hello dont les utilisateurs souhaité toosync toohello cluster. Par exemple, HiveUsers.
           
           Cliquez sur **sélectionnez** modifications de hello toosave.
           
           ![Configurer les paramètres du domaine du portail HDInsight joint](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Réseau virtuel** : contosohdivnet
       * **Sous-réseau** : Subnet1
         
         Cliquez sur **sélectionnez** modifications de hello toosave.        
         Cliquez sur **sélectionnez** modifications de hello toosave.
   * **Groupe de ressources**: groupe de ressources hello sélectionnez utilisé pour hello HDInsight VNet (contosohdirg).
4. Cliquez sur **Créer**.  

Une autre option pour créer le cluster HDInsight de domaine est un modèle de gestion des ressources Azure toouse. Hello procédure vous montre comment :

**toocreate un cluster HDInsight de domaine à l’aide d’un modèle de gestion des ressources**

1. Cliquez sur hello suivant image tooopen un modèle de gestionnaire de ressources Bonjour portail Azure. modèle de gestionnaire de ressources Hello se trouve dans un conteneur d’objets blob publics. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. À partir de hello **paramètres** panneau, entrez hello valeurs suivantes :
   
   * **Abonnement** : (sélectionnez votre abonnement Azure.)
   * **Groupe de ressources**: cliquez sur **utiliser l’existante**et spécifiez hello vous avez été à l’aide du même groupe de ressources.  Par exemple, contosohdirg. 
   * **Emplacement** : spécifiez un emplacement de groupe de ressources.
   * **Nom du cluster**: entrez un nom pour le cluster Hadoop hello que vous allez créer. Par exemple, contosohdicluster.
   * **Type de cluster** : sélectionnez un type de cluster.  la valeur par défaut Hello est **hadoop**.
   * **Emplacement**: sélectionnez un emplacement pour le cluster de hello.  compte de stockage par défaut Hello utilise hello même emplacement.
   * **Nombre de nœuds de travail de cluster**: sélectionnez nombre hello de nœuds de travail.
   * **Nom de connexion et mot de passe de cluster**: nom de connexion par défaut hello est **admin**.
   * **Mot de passe et le nom d’utilisateur SSH**: nom d’utilisateur par défaut de hello est **sshuser**.  Vous pouvez le renommer. 
   * **ID réseau virtuel** : /subscriptions/&lt;SubscriptionID&gt;/resourceGroups/&lt;ResourceGroupName&gt;/providers/Microsoft.Network/virtualNetworks/&lt;VNetName&gt;
   * **Sous-réseau du réseau virtuel** : /subscriptions/&lt;SubscriptionID&gt;/resourceGroups/&lt;ResourceGroupName&gt;/providers/Microsoft.Network/virtualNetworks/&lt;VNetName&gt;/subnets/Subnet1
   * **Nom de domaine** : contoso.onmicrosoft.com
   * **Organization Unit DN (Nom de domaine de l’unité d’organisation)** : UO = HDInsightOU,CD = contoso, CD = onmicrosoft, CD = com
   * **Nom de domaine du groupe d’utilisateurs du cluster** : [\"HiveUsers\"]
   * **LDAPUrls** : ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (entrée hello admin utilisateur nom de domaine)
   * **DomainAdminPassword**: (entrez hello domaine mot de passe administrateur)
   * **J’accepte les termes du contrat de toohello et conditions susmentionnées**: (Check)
   * **Code confidentiel toodashboard**: (Check)
3. Cliquez sur **Achat**. Vous verrez une nouvelle vignette intitulée **Déploiement du déploiement de modèle**. Cela prend environ environ 20 minutes toocreate un cluster. Une fois que le cluster de hello est créé, vous pouvez cliquer sur Panneau de cluster hello dans tooopen de portail hello il.

Après avoir terminé le didacticiel de hello, vous pourriez cluster hello de toodelete. Avec HDInsight, vos données sont stockées Azure Storage, pour que vous puissiez supprimer un cluster en toute sécurité s’il n’est pas en cours d’utilisation. Vous devez également payer pour un cluster HDInsight, même lorsque vous ne l’utilisez pas. Étant donné que les frais de hello pour le cluster de hello sont autant de fois plus de frais hello pour le stockage, il est judicieux économique toodelete clusters lorsqu’ils ne sont pas en cours d’utilisation. Pour obtenir des instructions de hello de la suppression d’un cluster, consultez [Hadoop de gérer les clusters dans HDInsight à l’aide de hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Étapes suivantes
* Pour configurer des stratégies Hive et exécuter des requêtes Hive, consultez [Configuration de stratégies Hive pour les clusters HDInsight joints à un domaine](hdinsight-domain-joined-run-hive.md).
* Pour utiliser des clusters SSH tooconnect appartenant à tooDomain HDInsight, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux, Unix et OS X](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

