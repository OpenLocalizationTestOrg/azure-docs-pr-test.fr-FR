---
title: "aaaReplicate un serveur IIS à plusieurs niveaux en fonction d’application web à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooreplicate IIS web des machines virtuelles de batterie de serveurs à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>Répliquer une application web multiniveau basée sur IIS à l’aide d’Azure Site Recovery

## <a name="overview"></a>Vue d'ensemble


Logiciel d’application est un moteur hello de productivité de l’entreprise dans une organisation. Des applications web diverses peuvent répondre aux différents besoins d’une organisation. Certaines, comme les applications de traitement des salaires et les applications financières, ainsi que les sites web destinés aux clients peuvent être de la plus grande importance pour une organisation. Il est important pour hello organisation toohave d’et en cours d’exécution à la perte de tooprevent toutes les heures de productivité et plus important encore empêchent d’une image de marque toohello dommages de l’organisation de hello.

Les applications web critiques sont généralement configurées en tant qu’applications multiniveau avec web de hello, d’une base de données et d’applications sur différents niveaux. Outre sont réparties entre plusieurs couches, hello applications peuvent également utiliser plusieurs serveurs dans chaque couche tooload équilibrer hello du trafic. En outre, les mappages entre les différents niveaux et sur le serveur web de hello de hello peuvent reposer sur des adresses IP statiques. Lors du basculement, certaines de ces mappages devez toobe mis à jour, en particulier, si vous avez plusieurs sites Web configurés sur le serveur web de hello. En cas d’applications web à l’aide de SSL, les liaisons de certificat devra toobe mis à jour.

Méthodes de récupération de base sans réplication traditionnel impliquent la sauvegarde de différents fichiers de configuration, paramètres du Registre, liaisons, des composants personnalisés (COM ou .NET), contenu et également les certificats et récupération hello fichiers via un ensemble d’étapes manuelles. Ces techniques sont clairement fastidieuses, sujettes aux erreurs et non évolutives. Il est, par exemple, facilement possible pour tooforget sauvegarde des certificats et rester avec aucun choix, mais toobuy nouveaux certificats pour le serveur de hello après le basculement.

Une solution de récupération d’urgence, devraient permettre la modélisation des plans de récupération autour hello au-dessus des architectures d’applications complexes et également avoir hello capacité tooadd personnalisé étapes toohandle mappages d’application entre les différents niveaux assurant ainsi une par simple clic que capture la solution dans l’événement hello d’un sinistre début tooa diminuer RTO.


Cet article décrit comment tooprotect un IIS en fonction à l’aide de web application un [Azure Site Recovery](site-recovery-overview.md). Cet article couvre les meilleures pratiques pour la réplication d’un à trois niveaux en fonction de IIS tooAzure d’application web, comment vous pouvez effectuer un exercice de récupération d’urgence, et comment vous pouvez basculement hello application tooAzure.


## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous que vous comprenez les suivant hello :

1. [Réplication d’un tooAzure de machine virtuelle](site-recovery-vmware-to-azure.md)
1. Comment trop[concevoir un réseau de récupération](site-recovery-network-design.md)
1. [Effectuer un tooAzure de basculement de test](./site-recovery-test-failover-to-azure.md)
1. [Effectuer un basculement tooAzure](site-recovery-failover.md)
1. Comment trop[répliquer un contrôleur de domaine](site-recovery-active-directory.md)
1. Comment trop[répliquer de SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Modèles de déploiement
Une application web IIS en fonction suit généralement une des hello suivant des modèles de déploiement :

**Modèle de déploiement 1** Une batterie de serveurs web IIS avec ARR (Application Request Routing), un serveur IIS et Microsoft SQL Server.

![Modèle de déploiement](./media/site-recovery-iis/deployment-pattern1.png)

**Modèle de déploiement 2** Une batterie de serveurs web IIS avec ARR (Application Request Routing), un serveur IIS, un serveur d’applications et Microsoft SQL Server.


![Modèle de déploiement](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Prise en charge de Site Recovery

À des fins de hello de la création de cet article les ordinateurs virtuels VMware avec le serveur IIS version 7.5 sur Windows Server 2012 R2, Enterprise ont été utilisés. Réplication de récupération de site est agnostique en termes d’application, les recommandations hello fournies ici sont toohold attendu sur également les scénarios suivants et pour une autre version d’IIS.

### <a name="source-and-target"></a>Source et cible

**Scénario** | **site secondaire de tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Oui | Oui
**VMware** | Oui | Oui
**Serveur physique** | Non | Oui

## <a name="replicate-virtual-machines"></a>Répliquer des machines virtuelles

Suivez [ce guide](site-recovery-vmware-to-azure.md) toostart répliquer tous les hello IIS web batterie de serveurs virtuels tooAzure.

Si vous utilisez une adresse IP statique, puis spécifiez IP hello souhaité hello tootake de machine virtuelle Bonjour [ **adresse IP cible** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) définition de paramètres de calcul et réseau.

![IP cible](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>Création d’un plan de récupération

Un plan de récupération permet de séquençage hello de basculement de différents niveaux dans une application multicouche, par conséquent, de maintenir la cohérence des applications. Lors de la création d’un plan de récupération pour une application web multicouche, suivez hello étapes ci-dessous.  [En savoir plus sur la création d’un plan de récupération](./site-recovery-create-recovery-plans.md).

### <a name="adding-virtual-machines-toofailover-groups"></a>Ajout de groupes de machines virtuelles toofailover
Une application web IIS à plusieurs niveaux typique se compose d’un niveau de base de données avec SQL machines virtuelles, niveau de web hello constituée par un serveur IIS et une couche application. Ajoutez toutes ces machines virtuelles toodifferent de groupe en fonction de la couche, comme ci-dessous. [En savoir plus sur la personnalisation du plan de récupération](site-recovery-runbook-automation.md#customize-the-recovery-plan).

1. Créez un plan de récupération. Ajoutez hello ordinateurs virtuels de niveau base de données sous le groupe 1 tooensure qu’ils sont arrêtés dernière et mis en premier.

1. Ajouter application hello hiérarchiser les machines virtuelles du groupe 2 où ils sont appelés après de la couche de base de données hello a été placée en.

1. Ajoutez hello web hiérarchiser les machines virtuelles dans le groupe 3 tels qu’ils sont appelés après de la couche d’application hello a été placée en.

1. Ajoutez équilibrer la charge des machines virtuelles dans le groupe 4 tels qu’ils sont appelés après mise niveau de hello web.


### <a name="adding-scripts-toohello-recovery-plan"></a>Ajout de scripts de plan de récupération toohello
Vous devrez peut-être toodo certaines opérations sur hello fonction de batterie de serveurs web basculement toomake IIS machines virtuelles post/Test de basculement correctement. Vous pouvez automatiser l’opération de basculement hello post telles que la mise à jour des entrées DNS, la modification de la liaison de site, des modifications dans la chaîne de connexion en ajoutant des scripts correspondant dans le plan de récupération hello comme indiqué ci-dessous. [En savoir plus sur l’ajout de scripts dans un plan de récupération](./site-recovery-create-recovery-plans.md#add-scripts).

#### <a name="dns-update"></a>Mise à jour DNS
Si hello DNS est configuré pour une mise à jour DNS dynamique de machines virtuelles généralement mettre à jour hello DNS avec la nouvelle adresse IP de hello une fois qu’ils démarrent. Tooadd un tooupdate étape explicite DNS avec hello nouvelles adresses IP d’ordinateurs virtuels hello puis ajouter ce [tooupdate adresse IP dans DNS de script](https://aka.ms/asr-dns-update) comme une action sur les groupes de plan de récupération.  

#### <a name="connection-string-in-an-applications-webconfig"></a>Chaîne de connexion dans le fichier web.config d’une application
chaîne de connexion Hello spécifie la base de données hello hello du site web communique avec.

Si la chaîne de connexion hello porte le nom hello d’ordinateur virtuel de base de données hello, aucune étape supplémentaire n’est nécessaire après basculement et application hello pourront tooautomatically communiquer toohello DB. En outre, si l’adresse IP de hello pour l’ordinateur virtuel de base de données hello est conservé, il ne sera pas nécessaire de chaîne de connexion tooupdate hello. Si la chaîne de connexion hello fait référence toohello de base de données virtual machine à l’aide d’une adresse IP, vous devez toobe mis à jour après basculement. Par exemple, Hello ci-dessous des chaîne de connexion pointe toohello DB avec IP 127.0.1.2

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

Vous pouvez mettre à jour de chaîne de connexion hello dans la couche web en ajoutant [script de mise à jour de connexion IIS](https://aka.ms/asr-update-webtier-script-classic) après le groupe 3 dans le plan de récupération hello.

#### <a name="site-bindings-for-hello-application"></a>Liaisons de site pour l’application hello
Chaque site se compose d’informations qui incluent le type hello de liaison, adresse IP de hello quels hello serveur IIS écoute les demandes de toohello pour le site de hello, numéro de port hello et noms d’hôte hello pour le site de hello de liaison. Au moment de hello d’un basculement, ces liaisons peut-être toobe mis à jour s’il existe une modification de l’adresse IP de hello qui s’y rapportent.

> [!NOTE]
>
> Si vous avez marqué « non assigné' pour la liaison de site hello comme exemple hello ci-dessous, il est inutile tooupdate ce basculement post de liaison. En outre, si l’adresse IP de hello associé à un site n’est pas modifiée après basculement, la liaison de site hello ne doive pas être mis à jour (rétention de l’adresse IP de hello dépend de l’architecture en réseau hello et sous-réseaux affecté toohello les sites principaux et de restauration et donc peuvent ou ne peuvent possible pour votre organisation.)

![Liaison SSL](./media/site-recovery-iis/sslbinding.png)

Si vous avez associé l’adresse IP de hello avec un site, vous devez tooupdate toutes les liaisons de site avec l’adresse IP de la nouvelle hello. Vous pouvez ajouter [script de mise à jour de couche Web IIS](https://aka.ms/asr-web-tier-update-runbook-classic) après les liaisons de site de récupération plan toochange hello, groupe 3.


#### <a name="update-load-balancer-ip-address"></a>Mettre à jour l’adresse IP de l’équilibreur de charge
Si vous avez Application Request Routing un ordinateur virtuel, ajoutez [script de basculement ARR IIS](https://aka.ms/asr-iis-arrtier-failover-script-classic) après l’adresse IP de groupe 4 tooupdate hello.

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>liaison de certificat SSL Hello pour une connexion https
Sites Web peuvent avoir un certificat SSL associé qui permet de garantir une communication sécurisée entre le serveur Web de hello et navigateur de l’utilisateur hello. Si le site Web de hello dispose d’une connexion https et une adresse IP toohello de liaison de site https associé du serveur IIS de hello avec une liaison de certificat SSL, une nouvelle liaison de site devez toobe ajoutée pour cert hello avec hello IP de l’ordinateur virtuel IIS hello valider le basculement.

certificat SSL de Hello peut être émise sur-

a) nom de domaine complet de hello du site Web de hello<br>
b) nom hello du serveur de hello<br>
c) d’un certificat générique pour le nom de domaine hello<br>
d) une adresse IP : si le certificat SSL de hello est émise sur IP hello du serveur IIS de hello, un autre toobe de besoins de certificat SSL émis par rapport à l’adresse IP de hello Hello serveur IIS sur hello site Azure et devez toobe créé une liaison SSL supplémentaire pour ce certificat. Par conséquent, il est conseillé de toonot un certificat SSL émis par rapport à IP. C’est une option moins couramment utilisée, qui sera bientôt dépréciée conformément aux nouvelles modifications du forum sur l’autorité de certification/navigateur.

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>Mettre à jour de la dépendance de hello entre web de hello et de la couche d’application hello
Si vous avez une dépendance d’application spécifique en fonction de l’adresse IP de hello d’ordinateurs virtuels hello, vous devez tooupdate ce basculement post de dépendance.

## <a name="doing-a-test-failover"></a>Exécution d’un test de basculement
Suivez [ce guide](site-recovery-test-failover-to-azure.md) toodo un test de basculement.

1.  TooAzure portail, sélectionnez le coffre de votre Service de récupération.
1.  Cliquez sur le plan de récupération hello créé pour la batterie de serveurs web IIS.
1.  Cliquez sur Test de basculement.
1.  Sélectionnez le point de récupération et le processus de basculement de test de réseau virtuel Azure toostart hello.
1.  Une fois les environnement secondaire hello, vous pouvez effectuer vos validations.
1.  Une fois les validations hello sont terminées, vous pouvez sélectionner 'Validations Terminer' et environnement de test de basculement hello est supprimé.

## <a name="doing-a-failover"></a>Exécution d’un basculement
Suivez [ce guide](site-recovery-failover.md) lorsque vous effectuez un basculement.

1.  TooAzure portail, sélectionnez le coffre de votre Service de récupération.
1.  Cliquez sur le plan de récupération hello créé pour la batterie de serveurs web IIS.
1.  Cliquez sur « Basculement ».
1.  Sélectionnez le processus de basculement de hello toostart de point de récupération.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez en savoir plus sur la [réplication d’autres applications](site-recovery-workload.md) à l’aide de Site Recovery.
