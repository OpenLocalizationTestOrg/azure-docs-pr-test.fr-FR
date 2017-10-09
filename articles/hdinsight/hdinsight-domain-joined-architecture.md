---
title: "architecture de Azure HDInsight appartenant à un aaaDomain | Documents Microsoft"
description: "Découvrez comment tooplan appartenant au domaine HDInsight."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Planifier des clusters Hadoop Azure joints à un domaine dans HDInsight

Hello Hadoop traditionnel est un cluster à utilisateur unique. Il convient à la plupart des entreprises qui font appel à des équipes d’application plus petites pour créer leurs charges de travail de données importantes. À mesure qu’Hadoop gagne en popularité, nombre d’entreprises font la transition vers un modèle dans lequel les clusters sont gérés par les équipes informatiques et partagés par plusieurs équipes d’application. Par conséquent, des clusters multi-utilisateur impliquant font partie des fonctionnalités hello plus fonctionnalités dans Azure HDInsight.

Au lieu de générer son propre authentification multi-utilisateur et l’autorisation, HDInsight s’appuie sur les plus populaires fournisseur d’identité hello--Active Directory (AD). fonctionnalités de sécurité puissant Hello dans Active Directory peuvent être utilisé toomanage des autorisation multi-utilisateur dans HDInsight. En intégrant HDInsight avec Active Directory, vous pouvez communiquer avec des clusters de hello à l’aide de vos informations d’identification Active Directory. HDInsight mappe un utilisateur Hadoop AD utilisateur tooa local, donc tous hello services s’exécutant sur HDInsight (Ambari, Hive Spark thrift de serveur, Ranger, serveur, etc.) fonctionnent en toute transparence pour l’utilisateur de hello authentifié.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Intégrer HDInsight à AD et AD sur la machine virtuelle IaaS

En intégrant HDInsight avec Azure AD ou AD sur Iaas VM, nœuds de cluster HDInsight hello sont joints au domaine de tooa domaine. HDInsight crée des principaux de service pour hello services Hadoop en cours d’exécution sur le cluster de hello et les place dans une unité d’organisation (UO) spécifiée dans Azure AD ou AD sur IaaS VM. HDInsight crée également les mappages DNS inverses dans le domaine hello pour hello adresses IP des nœuds hello toohello joint à un domaine.

Vous pouvez obtenir cette configuration en utilisant plusieurs architectures. Vous pouvez choisir parmi hello suivant des architectures.

**HDInsight intégré à AD fonctionnant sur Azure IaaS**

Il s’agit d’architecture de la plus simple de hello pour l’intégration de HDInsight avec Active Directory. Hello, contrôleur de domaine Active Directory s’exécute sur un (ou plusieurs) virtual machines virtuelles dans Azure. En général, ces machines virtuelles se trouvent sur un réseau virtuel. Permet de paramétrer un autre réseau virtuel pour le cluster HDInsight de hello. Pour HDInsight toohave un tooActive de ligne de vue active, vous devez toopeer ces réseaux virtuels à l’aide de [au réseau d’homologation](../virtual-network/virtual-network-create-peering.md). Si vous créez hello ARM, Active Directory, vous pouvez créer des hello Active Directory et HDInsight dans hello même réseau virtuel et vous n’avez pas besoin d’homologation de toodo. 

![Topologie du cluster HDInsight joint à un domaine](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> Dans cette architecture, vous ne pouvez pas utiliser Azure Data Lake Store avec le cluster HDInsight de hello.


Conditions préalables pour Active Directory :

* Un [unité d’organisation](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) doivent être créés, dans laquelle vous placez hello des machines virtuelles du cluster HDInsight et hello principaux de service utilisé par le cluster de hello.
* Les [protocoles LDAP (Lightweight Directory Access Protocol)](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) doivent être configurés pour communiquer avec AD. tooset du certificat utilisé Hello protocole LDAPS doit être un certificat réel (pas un certificat auto-signé).
* Les zones DNS inverses doivent être créés sur le domaine hello pour la plage d’adresses IP hello du sous-réseau de HDInsight hello (par exemple, 10.2.0.0/24 dans l’image précédente de hello).
* Un compte de service ou un compte d’utilisateur sont nécessaires. Utilisez ce cluster HDInsight de compte toocreate hello. Ce compte doit disposer de hello les autorisations suivantes :

    - Objets principal du service toocreate autorisations et les objets ordinateur dans l’unité d’organisation hello
    - Règles de proxy autorisations toocreate inversées DNS
    - Domaine Active Directory toohello autorisations toojoin machines

**HDInsight intégré à Azure AD dans le cloud uniquement**

Pour Azure AD dans le cloud uniquement, configurez un contrôleur de domaine pour que HDInsight puisse être intégré à Azure AD. Pour cela, vous devez utiliser [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS crée des ordinateurs de contrôleur de domaine sur le cloud de hello et fournit les adresses IP pour eux. Il crée deux contrôleurs de domaine pour la haute disponibilité.

Pour le moment, Azure AD DS existe uniquement dans les réseaux virtuels classiques. Il n’est accessible qu’à l’aide de hello portail Azure classic. Hello HDInsight réseau virtuel existe dans le portail Azure, qui doit toobe de hello homologuer avec un réseau virtuel hello classique à l’aide d’homologation de réseau virtuel à réseau virtuel.

> [!NOTE]
> Pour l’homologation entre un réseau virtuel classique et le réseau virtuel requiert que les deux réseaux virtuels est dans un gestionnaire de ressources Azure hello même région et sous hello même abonnement Azure.

![Topologie du cluster HDInsight joint à un domaine](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Composants requis pour Azure AD :

* Un [unité d’organisation](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) doivent être créées dans laquelle vous placez hello des machines virtuelles du cluster HDInsight et hello principaux de service utilisé par le cluster de hello.
* Le protocole [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) doit être paramétré lorsque vous configurez Azure AD DS. tooset du certificat utilisé Hello protocole LDAPS doit être un certificat réel (pas un certificat auto-signé).
* Les zones DNS inverses doivent être créés sur le domaine hello pour la plage d’adresses IP hello du sous-réseau de HDInsight hello (par exemple, 10.2.0.0/24 dans l’image précédente de hello).
* [Les hachages de mot de passe](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) doivent être synchronisés à partir d’Azure AD tooAzure les services AD DS.
* Un compte de service ou un compte d’utilisateur sont nécessaires. Utilisez ce cluster HDInsight de compte toocreate hello. Ce compte doit disposer de hello les autorisations suivantes :

    - Objets principal du service toocreate autorisations et les objets ordinateur dans l’unité d’organisation hello
    - Règles de proxy autorisations toocreate inversées DNS
    - Domaine d’autorisations toojoin machines toohello Azure AD

## <a name="next-steps"></a>Étapes suivantes
* tooconfigure un cluster HDInsight à un domaine, consultez [configurer appartenant au domaine des clusters HDInsight](hdinsight-domain-joined-configure.md).
* clusters HDInsight de toomanage appartenant au domaine, consultez [gérer appartenant au domaine des clusters HDInsight](hdinsight-domain-joined-manage.md).
* stratégies de ruche tooconfigure et exécution des requêtes Hive, consultez [Hive de configurer des stratégies pour joints au domaine des clusters HDInsight](hdinsight-domain-joined-run-hive.md).
* les requêtes de ruche toorun à l’aide de SSH sur des clusters HDInsight appartenant à un domaine, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
