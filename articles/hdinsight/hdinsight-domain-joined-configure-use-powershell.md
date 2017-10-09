---
title: "aaaConfigure des clusters HDInsight de domaine à l’aide de PowerShell - Azure | Documents Microsoft"
description: "Découvrez comment tooset installer et configurer des clusters HDInsight de domaine à l’aide d’Azure PowerShell"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Configurer des clusters HDInsight joints à un domaine (version préliminaire) à l’aide d’Azure PowerShell
Découvrez comment tooset d’un Azure HDInsight cluster avec Azure Active Directory (Azure AD) et [Apache Ranger](http://hortonworks.com/apache/ranger/) à l’aide d’Azure PowerShell. Un script Azure PowerShell est fourni toomake configuration de hello plus rapide et moins sujet aux erreurs. Le cluster HDInsight peut être configuré uniquement sur les clusters Linux. Pour plus d’informations, consultez [Introduire des clusters HDInsight joints à un domaine](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie n’est pas activé sur HDInsight joint à un domaine.

Une configuration de cluster HDInsight de domaine classique implique hello comme suit :

1. Créez un réseau virtuel Azure pour votre instance Azure AD.  
2. Créez et configurez Azure AD et Azure AD AS.
3. Ajouter une machine virtuelle toohello classique réseau virtuel pour la création d’une unité d’organisation. 
4. Créez une unité d’organisation pour Azure AD AS.
5. Créer un HDInsight VNet dans le mode de gestion des ressources Azure hello.
6. Le programme d’installation de zones DNS inverse pour hello Azure AD DS.
7. Homologue hello deux réseaux virtuels.
8. Créez un cluster HDInsight.

Hello script PowerShell fourni effectue les étapes 3 à 7. Vous devez effectuer les étapes 1 et 2 manuellement.  Si vous ne préférez pas toouse Azure PowerShell, consultez [clusters appartenant à un domaine de configurer les HDInsight](hdinsight-domain-joined-configure.md). 

Un exemple de topologie finale de hello se présente comme suit :

![Topologie HDInsight jointe à un domaine](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Azure AD ne prenant en charge que les réseaux virtuels Classic et les clusters HDInsight Linux ne prenant en charge que les réseaux virtuels Azure Resource Manager, l’intégration HDInsight Azure AD requiert deux réseaux virtuels et une homologation mutuelle. Pour plus d’informations hello comparaison entre les modèles de déploiement hello deux, consultez [Azure Resource Manager et déploiement classique : comprendre les modèles de déploiement et état de vos ressources de hello](../azure-resource-manager/resource-manager-deployment-model.md). Hello deux réseaux virtuels doivent être Bonjour même région que hello Azure AD DS.

> [!NOTE]
> Ce didacticiel part du principe que vous ne possédez pas d’instance Azure AD. Si vous avez un, vous pouvez ignorer la partie hello à l’étape 2.
> 
> 

## <a name="prerequisites"></a>Composants requis
Vous devez avoir hello suivant toogo d’éléments dans ce didacticiel :

* Familiarisez-vous avec les [services de domaine Azure AD](https://azure.microsoft.com/services/active-directory-ds/), et la structure de [tarification](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Assurez-vous que votre abonnement est dans la liste approuvée de cette version préliminaire publique. Vous pouvez le faire en envoyant un e-mail toohdipreview@microsoft.com avec votre ID d’abonnement.
* Un certificat SSL signé par une autorité signataire pour votre domaine. certificat de Hello est requise par la configuration de LDAP sécurisé. Les certificats auto-signés ne peuvent pas être utilisés.
* Azure PowerShell.  Consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Créez un réseau virtuel Azure pour votre instance Azure AD.
Pour obtenir des instructions de hello, consultez [ici](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Créez et configurez Azure AD et Azure AD AS.
Pour obtenir des instructions de hello, consultez [ici](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Exécutez le script PowerShell de hello
Hello script PowerShell peut être téléchargé à partir de [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Extrayez le fichier zip de hello et enregistrer localement les fichiers hello.

**tooedit hello script PowerShell**

1. Ouvrez run.ps1 à l’aide de Windows PowerShell ISE ou n’importe quel éditeur de texte.
2. Remplir les valeurs hello pour hello suivant variables :
   
   * **$SubscriptionName** : hello nom Hello abonnement Azure où vous souhaitez toocreate votre cluster HDInsight. Vous avez déjà créé un réseau virtuel classique dans cet abonnement et création d’un réseau virtuel Azure Resource Manager pour le cluster HDInsight de hello sous l’abonnement.
   * **$ClassicVNetName** -hello classique un réseau virtuel qui contient hello Azure AD DS. Ce réseau virtuel doit être Bonjour même abonnement qui est fourni ci-dessus. Ce réseau virtuel doit être créé à l’aide de hello portail Azure et ne pas à l’aide de portail classique. Si vous suivez les instructions de hello de [les clusters HDInsight de configuration à un domaine (version préliminaire)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), nom par défaut de hello est contosoaadvnet.
   * **$ClassicResourceGroupName** – nom du groupe hello Gestionnaire de ressources pour hello classique réseau virtuel qui est mentionnée ci-dessus. Par exemple contosoaadrg. 
   * **$ArmResourceGroupName** – nom de groupe de ressources hello qui vous voulez toocreate hello HDInsight cluster. Vous pouvez utiliser hello même groupe de ressources en tant que $ArmResourceGroupName.  Si le groupe de ressources hello n’existe pas, le script de hello crée groupe de ressources hello.
   * **$ArmVNetName** -nom de réseau virtuel de gestionnaire de ressources hello dans laquelle vous souhaitez le cluster HDInsight de hello toocreate. Ce réseau virtuel sera placé dans $ArmResourceGroupName.  Si hello réseau virtuel n’existe pas, hello script PowerShell crée. S’il n’existe pas, il doit faire partie hello du groupe de ressources que vous fournissez ci-dessus.
   * **$AddressVnetAddressSpace** : hello espace d’adressage de réseau virtuel du Gestionnaire de ressources hello du réseau. Assurez-vous que cet espace d’adressage est disponible. Cet espace d’adressage ne peut pas chevaucher l’espace d’adressage hello classique du réseau virtuel. Par exemple : “10.1.0.0/16”
   * **$ArmVnetSubnetName** -nom de sous-réseau hello Gestionnaire de ressources du réseau virtuel dans lequel vous souhaitez les machines virtuelles de cluster HDInsight tooplace hello. Si le sous-réseau de hello n’existe pas, hello script PowerShell crée. S’il n’existe pas, il doit faire partie du réseau virtuel hello que vous fournissez ci-dessus.
   * **$AddressSubnetAddressSpace** : hello plage d’adresses de sous-réseau de réseau virtuel hello Gestionnaire de ressources du réseau. Bonjour cluster HDInsight seront des adresses IP de VM à partir de cette plage d’adresses de sous-réseau. Par exemple : “10.1.0.0/24”.
   * **$ActiveDirectoryDomainName** – machines virtuelles de cluster de nom de domaine hello Azure AD que vous souhaitez toojoin hello HDInsight. Par exemple, “contoso.onmicrosoft.com”
   * **$ClusterUsersGroups** – nom commun de hello hello des groupes de sécurité à partir d’Active Directory que vous souhaitez toosync toohello HDInsight cluster. les utilisateurs de Hello au sein de ce groupe de sécurité seront en mesure de toolog sur toohello tableau de bord de cluster à l’aide de leurs informations d’identification de domaine active directory. Ces groupes de sécurité doivent exister dans active directory de hello. Par exemple, « hiveusers » ou « clusteroperatorusers ».
   * **$OrganizationalUnitName** -unité d’organisation dans le domaine hello, dans lequel vous souhaitez que les machines virtuelles de cluster HDInsight tooplace hello et hello principaux de service utilisé par le cluster de hello hello. Hello script PowerShell crée cette unité d’organisation si elle n’existe pas. Par exemple, « HDInsightOU ».
3. Enregistrer les modifications de hello.

**script de hello toorun**

1. Exécutez **Windows PowerShell** en tant qu’administrateur.
2. Parcourir le dossier toohello de run.ps1. 
3. Exécutez le script de hello en tapant le nom de fichier hello et d’accès **entrée**.  3 boîtes de dialogue de connexion s’affichent :
   
   1. **Connectez-vous au portail classique de tooAzure** – Entrez vos informations d’identification que vous pouvez utiliser toosign dans le portail classique de tooAzure. Vous devez avoir créé hello Azure AD et Azure AD DS à l’aide de ces informations d’identification.
   2. **Connectez-vous au portail de gestion de ressources tooAzure** – Entrez vos informations d’identification que vous pouvez utiliser toosign dans tooAzure Gestionnaire de ressources du portail.
   3. **Nom d’utilisateur de domaine** – entrez hello les informations d’identification de nom d’utilisateur de domaine hello que vous souhaitez toobe un administrateur de cluster HDInsight de hello. Si vous avez créé un répertoire Azure AD à partir de rien, vous devez avez probablement créé cet utilisateur à l’aide de cette documentation. 
      
      > [!IMPORTANT]
      > Entrez le nom d’utilisateur hello sous la forme : 
      > 
      > Nomdomaine\nomutilisateur (par exemple contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      Cet utilisateur doit disposer des 3 privilèges : toojoin machines toohello fourni de domaine Active Directory ; toocreate principaux du service et des objets ordinateur dans hello fourni à une unité d’organisation ; et tooadd des règles de proxy inverses DNS.

Lors de la création zones DNS inversées, script de hello vous invitera tooenter un ID de réseau. Cet ID de réseau doit être le préfixe d’adresse du réseau de le virtuel hello Gestionnaire de ressources. Par exemple, si l’espace d’adressage du sous-réseau de réseau virtuel de votre gestionnaire de ressources est 10.2.0.0/24, entrez 10.2.0.0/24 lors de l’outil de hello vous invite à entrer les ID de réseau hello. 

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
     * **Version** : Hadoop 2.7.3 (HDI 3.5). Le cluster HDInsight joint au domaine est pris en charge uniquement sur le cluster HDInsight version 3.5.
     * **Type de cluster** : PREMIUM
       
       Cliquez sur **sélectionnez** modifications de hello toosave.
   * **Informations d’identification**: hello informations d’identification utilisateur de cluster hello et utilisateur SSH hello.
   * **Source de données**: créer un nouveau compte de stockage ou utiliser un compte de stockage existant comme compte de stockage par défaut pour le cluster HDInsight de hello de hello. emplacement de Hello doit être hello identique hello deux réseaux virtuels.  emplacement de Hello est également hello du cluster HDInsight de hello.
   * **Tarification**: sélectionnez nombre hello de nœuds de travail de votre cluster.
   * **Configurations avancées** : 
     
     * **Jonction de domaine et réseau virtuel/sous-réseau** : 
       
       * **Paramètres du domaine** : 
         
         * **Nom du domaine** : contoso.onmicrosoft.com
         * **Mot de passe utilisateur du domaine** :saisissez un nom d’utilisateur du domaine. Ce domaine doit avoir hello suivant des privilèges : joindre machines toohello domaine et les placer dans l’unité d’organisation hello configuré précédemment ; Créer des principaux de service au sein de l’unité d’organisation hello configuré précédemment ; Créer des entrées DNS inverses. Cet utilisateur de domaine devient administrateur hello de ce cluster HDInsight appartenant au domaine.
         * **Mot de passe de domaine**: entrez le mot de passe utilisateur de domaine hello.
         * **Unité d’organisation**: entrez hello le nom unique de hello unité d’organisation que vous avez configuré précédemment. Par exemple : UO = HDInsightOU, CD = contoso, CD = onmicrosoft, CD = com
         * **URL LDAPS** : ldaps://contoso.onmicrosoft.com:636
         * **Groupe d’utilisateurs accès**: spécifiez le groupe de sécurité hello dont les utilisateurs que vous voulez toosync toohello cluster. Par exemple, HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **Cluster Users Group D Ns**: "\"NC = HiveUsers, UO = AADDC Users,CD =<DomainName>, CD = onmicrosoft,CD = com\""
   * **LDAPUrls** : ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (entrée hello admin utilisateur nom de domaine)
   * **DomainAdminPassword**: (entrez hello domaine mot de passe administrateur)
   * **J’accepte les termes du contrat de toohello et conditions susmentionnées**: (Check)
   * **Code confidentiel toodashboard**: (Check)
3. Cliquez sur **Achat**. Vous verrez une nouvelle vignette intitulée **Déploiement du déploiement de modèle**. Cela prend environ environ 20 minutes toocreate un cluster. Une fois que le cluster de hello est créé, vous pouvez cliquer sur Panneau de cluster hello dans tooopen de portail hello il.

Après avoir terminé le didacticiel de hello, vous pourriez cluster hello de toodelete. Avec HDInsight, vos données sont stockées Azure Storage, pour que vous puissiez supprimer un cluster en toute sécurité s’il n’est pas en cours d’utilisation. Vous devez également payer pour un cluster HDInsight, même lorsque vous ne l’utilisez pas. Étant donné que les frais de hello pour le cluster de hello sont autant de fois plus de frais hello pour le stockage, il est judicieux économique toodelete clusters lorsqu’ils ne sont pas en cours d’utilisation. Pour obtenir des instructions de hello de la suppression d’un cluster, consultez [Hadoop de gérer les clusters dans HDInsight à l’aide de hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Étapes suivantes

* Pour configurer des stratégies Hive et exécuter des requêtes Hive, consultez [Configuration de stratégies Hive pour les clusters HDInsight joints à un domaine](hdinsight-domain-joined-run-hive.md).
* Pour utiliser des clusters SSH tooconnect appartenant à tooDomain HDInsight, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

