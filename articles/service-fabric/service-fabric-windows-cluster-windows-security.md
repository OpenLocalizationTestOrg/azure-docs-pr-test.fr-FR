---
title: "aaaSecure un cluster exécutant Windows à l’aide de la sécurité Windows | Documents Microsoft"
description: "Découvrez comment tooconfigure nœud à nœud et client à l’autre la sécurité sur un serveur autonome de cluster en cours d’exécution sur Windows à l’aide de la sécurité de Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Sécuriser un cluster autonome sous Windows avec la sécurité Windows
tooprevent non autorisé cluster Service Fabric de tooa accès, vous devez sécuriser le cluster de hello. Sécurité est particulièrement importante lorsque le cluster de hello exécutant des charges de travail de production. Cet article décrit la sécurité de nœud à nœud et client à nœud tooconfigure Bonjour à l’aide de la sécurité Windows *ClusterConfig.JSON* fichier.  processus de Hello correspond toohello configurer l’étape de sécurité de [créer un cluster autonome s’exécutant sous Windows](service-fabric-cluster-creation-for-windows-server.md). Pour plus d’informations sur la manière dont Service Fabric utilise la sécurité Windows, référez-vous à [Scénarios de sécurité du cluster](service-fabric-cluster-security.md).

> [!NOTE]
> Vous devez envisager sélection hello de sécurité du nœud à l’autre avec précaution, car il n’existe aucune mise à niveau de cluster à partir d’un tooanother de choix de sécurité. sélection de sécurité toochange hello, vous avez cluster complet de toorebuild hello.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Configuration de la sécurité Windows à l’aide de gMSA  
exemple Hello *ClusterConfig.gMSA.Windows.MultiMachine.JSON* fichier de configuration téléchargés avec hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) package de cluster autonome contient un modèle de configuration de sécurité de Windows à l’aide [groupe des comptes de Service administré (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Paramètres de configuration** | **Description** |  
| --- | --- |  
| WindowsIdentities |Contient les identités de cluster et le client hello. |  
| ClustergMSAIdentity |Configure la sécurité nœud à nœud. Un compte de service géré de groupe. |  
| ClusterSPN |Nom principal de service de domaine complet pour le compte de service géré de groupe|  
| ClientIdentities |Configure la sécurité client à nœud. Tableau des comptes d’utilisateur du client. |  
| Identité |identité du client Hello, un utilisateur de domaine. |  
| IsAdmin |La valeur True indique que cet utilisateur de domaine hello a l’accès administrateur client, false pour l’accès client utilisateur. |  
  
[Sécurité du nœud toonode](service-fabric-cluster-security.md#node-to-node-security) est configuré en définissant **ClustergMSAIdentity** quand service fabric doit toorun sous service administré de groupe. Dans l’ordre toobuild relations d’approbation entre nœuds, ils doivent être informés de l’autre. Cela peut être accompli de deux manières différentes : spécifiez hello groupe compte de Service administré qui inclut tous les nœuds de cluster de hello ou groupe d’ordinateurs de domaine hello qui inclut tous les nœuds de cluster de hello. Nous vous recommandons fortement de l’utilisation de hello [groupe des comptes de Service administré (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approche, en particulier pour les clusters de grande taille (plus de 10 nœuds) ou pour les clusters qui sont susceptibles de toogrow ou la réduction.  
Cette approche ne nécessite pas la création d’un groupe de domaine pour lequel les administrateurs de cluster ont été accordées tooadd de droits d’accès et supprimer des membres hello. Ces comptes sont également utiles pour la gestion des mots de passe automatique. Pour en savoir plus, consultez [Prise en main des comptes de service gérés de groupe](http://technet.microsoft.com/library/jj128431.aspx).  
 
[Sécurité de client toonode](service-fabric-cluster-security.md#client-to-node-security) est configuré à l’aide de **ClientIdentities**. Commande tooestablish une confiance entre le client et hello cluster, vous devez configurer hello cluster tooknow les identités de client qu’il peut faire confiance. Cela est possible de deux manières différentes : spécifiez les utilisateurs du groupe domaine hello qui peuvent se connecter ou spécifiez hello utilisateurs de nœud de domaine qui peuvent se connecter. L’infrastructure de service prend en charge deux types de contrôle d’accès différents pour les clients qui sont connectés tooa Service Fabric clusters : administrateur et utilisateur. Contrôle d’accès permet hello hello cluster administrateur toolimit accès toocertain types d’opérations de cluster pour différents groupes d’utilisateurs, la sécurisation de cluster de hello.  Les administrateurs disposent de fonctionnalités de toomanagement d’un accès complet (y compris les fonctionnalités en lecture/écriture). Les utilisateurs, par défaut, ont uniquement un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête), hello capacité tooresolve applications et services. Pour en savoir plus sur les contrôles d’accès, consultez [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric](service-fabric-cluster-security-roles.md).  
 
Hello selon exemple **sécurité** section configure la sécurité de Windows à l’aide de service administré de groupe et spécifie que hello machines dans *ServiceFabric.clusterA.contoso.com* gMSA font partie du cluster de hello et que *CONTOSO\usera* dispose d’un accès administrateur client :  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Configuration de la sécurité Windows à l’aide d’un groupe de machines  
exemple Hello *ClusterConfig.Windows.MultiMachine.JSON* fichier de configuration téléchargés avec hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) package de cluster autonome contient un modèle de configuration de la sécurité de Windows.  La sécurité de Windows est configurée dans hello **propriétés** section : 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Paramètre de configuration** | **Description** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** est défini trop*Windows* si ClusterIdentity spécifie un nom de groupe ordinateur Active Directory. |  
| ServerCredentialType |Définir trop*Windows* tooenable sécurité Windows pour les clients.<br /><br />Cela indique que les clients hello de hello et le cluster hello lui-même sont exécutent dans un domaine Active Directory. |  
| WindowsIdentities |Contient les identités de cluster et le client hello. |  
| ClusterIdentity |Utiliser un nom de groupe ordinateur, la domain\machinegroup, la sécurité du nœud à l’autre tooconfigure. |  
| ClientIdentities |Configure la sécurité client à nœud. Tableau des comptes d’utilisateur du client. |  
| Identité |Ajouter un utilisateur de domaine hello, DOMAINE\nom d’utilisateur pour l’identité du client hello. |  
| IsAdmin |Jeu tootrue toospecify qui hello utilisateur de domaine a l’accès administrateur client ou false pour l’accès client utilisateur. |  

[Sécurité du nœud toonode](service-fabric-cluster-security.md#node-to-node-security) est configuré à l’aide de configuration **ClusterIdentity** si vous voulez toouse un groupe d’ordinateurs dans un domaine Active Directory. Pour en savoir plus, consultez la rubrique traitant de la [création d’un groupe de machines dans Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).

La [sécurité de client à nœud](service-fabric-cluster-security.md#client-to-node-security) est configurée avec **ClientIdentities**. tooestablish d’approbation entre un client et hello du cluster, vous devez configurer hello cluster tooknow hello client peuvent faire confiance à des identités hello cluster. Vous pouvez établir cette approbation de deux manières différentes :

- Spécifiez les utilisateurs de groupe de domaine hello qui peuvent se connecter.
- Spécifiez les utilisateurs de nœud de domaine de hello qui peuvent se connecter.

L’infrastructure de service prend en charge deux types de contrôle d’accès différents pour les clients qui sont connectés tooa Service Fabric clusters : administrateur et utilisateur. Contrôle d’accès permet hello cluster toolimit accès toocertain types d’administrateur d’opérations de cluster pour différents groupes d’utilisateurs, ce qui rend le cluster de hello plus sécurisé.  Les administrateurs disposent de fonctionnalités de toomanagement d’un accès complet (y compris les fonctionnalités en lecture/écriture). Les utilisateurs, par défaut, ont uniquement un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête), hello capacité tooresolve applications et services.  

Hello selon exemple **sécurité** section configure la sécurité de Windows, spécifie que hello machines dans *ServiceFabric/clusterA.contoso.com* font partie du cluster de hello et spécifie que  *CONTOSO\usera* dispose d’un accès administrateur client :

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> Service Fabric ne doit pas être déployé sur un contrôleur de domaine. Assurez-vous que ClusterConfig.json ne pas inclure l’adresse IP de hello hello du contrôleur de domaine lors de l’utilisation d’un groupe d’ordinateurs ou groupe compte de Service administré (gMSA).
>
>

## <a name="next-steps"></a>Étapes suivantes
Après la configuration de sécurité Windows Bonjour *ClusterConfig.JSON* de fichiers, reprendre le processus de création de cluster hello dans [créer un cluster autonome s’exécutant sous Windows](service-fabric-cluster-creation-for-windows-server.md).

Pour plus d’informations sur la sécurité de nœud à nœud, la sécurité de client à nœud et le contrôle d’accès en fonction du rôle, consultez la page [Scénarios relatifs à la sécurité des clusters](service-fabric-cluster-security.md).

Consultez [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md) pour obtenir des exemples de la connexion à l’aide de PowerShell ou fabricclient ne.
