---
title: "disponibilité aaaHigh avec la passerelle de gestion des données dans Azure Data Factory | Documents Microsoft"
description: "Cet article explique comment augmenter le nombre d’instances (scale out) d’une passerelle de gestion des données en ajoutant des nœuds et comment augmenter la taille des instances (scale up) en augmentant le nombre de travaux simultanés pouvant s’exécuter sur un nœud."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>Passerelle de gestion des données - Haute disponibilité et scalabilité (préversion)
Cet article vous aide à configurer la solution Haute disponibilité et scalabilité avec la passerelle de gestion des données.    

> [!NOTE]
> Cet article part du principe que vous connaissez déjà les bases de la passerelle de gestion des données. Si ce n’est pas le cas, consultez [Passerelle de gestion des données](data-factory-data-management-gateway.md).

>**Cette fonctionnalité en version préliminaire est officiellement prise en charge sur les versions 2.12.xxxx.x et ultérieures de la passerelle de gestion des données**. Assurez-vous que vous utilisez la version 2.12.xxxx.x ou une version supérieure. Télécharger la version la plus récente de la passerelle de gestion des données hello [ici](https://www.microsoft.com/download/details.aspx?id=39717).

## <a name="overview"></a>Vue d'ensemble
Vous pouvez associer des passerelles de gestion de données qui sont installés sur plusieurs ordinateurs locaux avec une seule passerelle logique à partir du portail de hello. Ces ordinateurs sont appelés **nœuds**. Vous pouvez utiliser jusqu'à trop**quatre nœuds** associé à une passerelle logique. avantages de Hello d’avoir plusieurs nœuds (machines locales avec la passerelle installée) pour une passerelle logique sont :  

- Les performances du déplacement des données entre les magasins de données locaux et dans le cloud sont améliorées.  
- Si un des nœuds de hello tombe en panne pour une raison quelconque, les autres nœuds sont toujours disponibles pour le déplacement des données de salutation. 
- Si un des nœuds de hello devez toobe hors connexion pour maintenance, les autres nœuds sont toujours disponibles pour le déplacement des données de salutation.

Vous pouvez également configurer le nombre de hello de **tâches de déplacement de données simultanées** qui peut s’exécuter sur un tooscale nœud capacité hello de déplacement de données locaux et cloud banques de données. 

À l’aide de hello portail Azure, vous pouvez surveiller l’état hello de ces nœuds, ce qui vous permet de décider si tooadd ou supprimer un nœud à partir de la passerelle de logique hello. 

## <a name="architecture"></a>Architecture 
Hello diagramme suivant présente hello architecture l’évolutivité et des fonctionnalités de disponibilité de hello passerelle de gestion des données : 

![Passerelle de gestion des données - Haute disponibilité et scalabilité](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

A **passerelle logique** passerelle hello ajouter de fabrique de données tooa Bonjour portail Azure. Avant, vous ne pouviez associer qu’un seul ordinateur Windows local doté d’une passerelle de gestion des données installée avec une passerelle logique. Cet ordinateur passerelle local est appelé nœud. Vous pouvez maintenant associer des trop**quatre nœuds physiques** avec une passerelle logique. Une passerelle logique dotée de plusieurs nœuds est appelée **passerelle à plusieurs nœuds**.  

Tous ces nœuds sont **actifs**. Tous les peuvent traiter les données de toomove de travaux de déplacement des données entre locaux et cloud banques de données. Un des nœuds de hello agissent en tant que le répartiteur et de travail. Autres nœuds dans les groupes de hello sont des nœuds de travail. A **répartiteur** nœud extrait des tâches/travaux de déplacement de données à partir du service de cloud computing hello et distribue les nœuds tooworker (y compris lui-même). A **travail** nœud exécute le déplacement des travaux toomove de données entre locaux et cloud banques de données. Tous les nœuds sont des rôles de travail. Un seul nœud peut être à la fois répartiteur et rôle de travail.    

Vous pouvez commencent généralement par un seul nœud et **montée en puissance parallèle** tooadd plus de nœuds hello ou des nœuds existants sont submergés par la charge de déplacement des données hello. Vous pouvez également **montée en puissance** hello la fonctionnalité de déplacement des données d’un nœud de passerelle en augmentant le nombre de hello de travaux simultanés autorisés toorun sur le nœud de hello. Cette fonctionnalité est également disponible avec une passerelle à un seul nœud (même quand la fonctionnalité de l’évolutivité et disponibilité hello n’est pas activée). 

Une passerelle avec plusieurs nœuds conserve les informations d’identification de magasin de données hello synchronisés sur tous les nœuds. S’il existe un problème de connectivité du nœud à l’autre, les informations d’identification hello peuvent être synchronisées. Lorsque vous définissez les informations d’identification pour un magasin de données local qui utilise une passerelle, il enregistre les informations d’identification sur le nœud de répartiteur/de travail hello. Hello répartiteur nœud se synchronise avec les autres nœuds de travail. Ce processus est appelé **synchronisation des informations d’identification**. le canal de communication hello entre les nœuds peut être **chiffrées** par un certificat SSL/TLS publique. 

## <a name="set-up-a-multi-node-gateway"></a>Configurer une passerelle à plusieurs nœuds
Cette section part du principe que vous avez parcouru hello suivant deux articles ou familiarisés avec les concepts dans les articles suivants : 

- [Passerelle de gestion des données](data-factory-data-management-gateway.md) -fournit une vue d’ensemble détaillée de la passerelle de hello.
- [Déplacer des données entre des magasins de données locaux et dans le cloud](data-factory-move-data-between-onprem-and-cloud.md) - contient une procédure pas à pas donnant des instructions sur l’utilisation d’une passerelle à nœud unique.  

> [!NOTE]
> Avant d’installer une passerelle de gestion des données sur un ordinateur local, Windows, consultez la configuration requise indiquée dans [article principal de hello](data-factory-data-management-gateway.md#prerequisites).

1. Bonjour [procédure pas à pas](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), lors de la création d’une passerelle logique, activer hello **haute disponibilité et évolutivité** fonctionnalité. 

    ![Passerelle de gestion des données - Haute disponibilité et scalabilité](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. Bonjour **configurer** page, utilisez **le programme d’installation Express** ou **le programme d’installation manuelle** lien tooinstall une passerelle sur le nœud de premier hello (un ordinateur local, Windows).

    ![Passerelle de gestion des données - Installation rapide ou manuelle](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Si vous utilisez option d’installation rapide hello, la communication de nœud à nœud hello est effectuée sans chiffrement. nom du nœud Hello est identique au nom de l’ordinateur hello. Utilisez le programme d’installation manuelle si la communication de nœud à nœud de hello doit toobe chiffré ou que vous souhaitiez toospecify un nom de nœud de votre choix. Il n’est pas possible de modifier les noms de nœuds ultérieurement.
3. Si vous choisissez **Installation rapide** :
    1. Vous consultez hello suivant message une fois la passerelle de hello est correctement installé :

        ![Passerelle de gestion des données - Installation rapide terminée](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. Lancez le Gestionnaire de Configuration de gestion de données pour la passerelle de hello en suivant [ces instructions](data-factory-data-management-gateway.md#configuration-manager). Vous consultez le nom de la passerelle hello, nom de nœud, état, etc..

        ![Passerelle de gestion des données - Installation terminée](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. Si vous choisissez **Installation manuelle** :
    1. Télécharger le package d’installation hello de hello Microsoft Download Center, tooinstall passerelle l’exécuter sur votre ordinateur.
    2. Hello d’utilisation **clé d’authentification** de hello **configurer** passerelle de page tooregister hello.
    
        ![Passerelle de gestion des données - Installation terminée](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. Bonjour **nouveau nœud de passerelle** page, vous pouvez fournir une personnalisée **nom** nœud de passerelle toohello. Par défaut, le nom du nœud est identique au nom de l’ordinateur hello.    

        ![Passerelle de gestion des données - Spécifier un nom](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. Dans la page suivante de hello, vous pouvez choisir si trop**activer le chiffrement pour la communication de nœud à l’autre**. Cliquez sur **ignorer** toodisable chiffrement (par défaut).

        ![Passerelle de gestion des données - Activer le chiffrement](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > La modification du mode de chiffrement est uniquement pris en charge lorsque vous avez un nœud de passerelle unique dans la passerelle de logique hello. mode de chiffrement toochange hello lorsqu’une passerelle a plusieurs nœuds, hello comme suit : supprimez tous les nœuds de hello, à l’exception d’un seul nœud, modifier le mode de chiffrement hello et puis ajoutez de nouveau les nœuds hello.
        > 
        > Consultez la section [Configuration requise des certificats TSL/SSL](#tlsssl-certificate-requirements) pour obtenir la liste des conditions préalables à l’utilisation d’un certificat TLS/SSL. 
    5. Une fois la passerelle de hello est correctement installé, cliquez sur lancer le Gestionnaire de Configuration :
    
        ![Installation manuelle - Lancer le Gestionnaire de configuration](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. vous voyez le Gestionnaire de Configuration de passerelle de gestion de données sur le nœud hello (ordinateur local, Windows), qui affiche l’état de connectivité, **nom de la passerelle**, et **nom de nœud**.  

        ![Passerelle de gestion des données - Installation terminée](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > Si vous configurez une passerelle hello sur une machine virtuelle Azure, vous pouvez utiliser [ce modèle Azure Resource Manager sur GitHub](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway). Ce script crée une passerelle logique, configure les ordinateurs virtuels équipés de logiciels de passerelle de gestion des données et les inscrit avec la passerelle de logique hello. 
6. Dans le portail Azure, lancez hello **passerelle** page : 
    1. Dans la page d’accueil fabrique hello données dans le portail de hello, cliquez sur **Services liés**.
    
        ![Page d'accueil Data Factory](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. Sélectionnez hello **passerelle** toosee hello **passerelle** page :
    
        ![Page d'accueil Data Factory](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. Vous consultez hello **passerelle** page :   

        ![Affichage de la passerelle à nœud unique](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. Cliquez sur **ajouter un nœud** sur la barre d’outils de hello tooadd une passerelle logique toohello de nœud. Si vous envisagez de l’installation rapide toouse, effectuez cette étape à partir de la machine locale hello qui est ajouté en tant que nœud toohello passerelle. 

    ![Passerelle de gestion des données - Menu Ajouter un nœud](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. Étapes sont semblables toosetting nœud de premier hello. Hello Configuration Manager UI vous permet de définir le nom du nœud hello si vous choisissez l’option d’installation manuelle de hello : 

    ![Gestionnaire de configuration - Installer une deuxième passerelle](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Une fois la passerelle de hello est correctement installé sur le nœud de hello, outil de Configuration Manager hello affiche hello suivant d’écran :  

    ![Gestionnaire de configuration - Installation de la deuxième passerelle terminée](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Si vous ouvrez hello **passerelle** page dans le portail hello, vous voyez maintenant deux nœuds de passerelle : 

    ![Passerelle avec deux nœuds dans le portail de hello](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete un nœud de passerelle, cliquez sur **supprimer un nœud** sur la barre d’outils de hello, sélectionnez le nœud de hello vous souhaitez toodelete, puis cliquez sur **supprimer** à partir de la barre d’outils hello. Cette action supprime le nœud sélectionné de hello du groupe de hello. Notez que cette action ne désinstalle pas le logiciel de passerelle de gestion de données hello à partir du nœud de hello (ordinateur local, Windows). Utilisez **ajouter ou supprimer des programmes** dans le panneau de configuration sur la passerelle de hello toouninstall hello localement. Lorsque vous désinstallez la passerelle à partir du nœud de hello, elle est automatiquement supprimée dans le portail de hello.   

## <a name="upgrade-an-existing-gateway"></a>Mettre à niveau une passerelle existante
Vous pouvez mettre à niveau un existant passerelle toouse hello haute disponibilité et la fonctionnalité d’extensibilité. Cette fonctionnalité fonctionne uniquement avec les nœuds ayant une passerelle de gestion des données hello de version > = 2.12.xxxx. Vous pouvez voir version hello de passerelle de gestion des données installé sur un ordinateur de hello **aide** onglet Hello Gestionnaire de Configuration de passerelle de gestion de données. 

1. Hello local machine toohello version la plus récente en suivant la passerelle hello mise à jour en téléchargeant et en exécutant un package d’installation MSI de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717). Consultez la section [Installation](data-factory-data-management-gateway.md#installation) pour plus d’informations.  
2. Accédez toohello portail Azure. Lancez hello **page de la fabrique de données** de votre fabrique de données. Cliquez sur lié services vignette toolaunch hello **page des services liés**. Hello de hello sélectionnez passerelle toolaunch **page de la passerelle**. Cliquez sur et activer **fonctionnalité en version préliminaire** comme indiqué dans hello suivant image : 

    ![Passerelle de gestion des données - Activer la fonctionnalité en préversion](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Une fois que la fonctionnalité d’aperçu hello est activée dans le portail de hello, fermez toutes les pages. Rouvrez hello **page de la passerelle** toosee hello nouvelle interface utilisateur d’aperçu (IU).
 
    ![Passerelle de gestion des données - Activation de la fonctionnalité en préversion terminée](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![Passerelle de gestion des données - Interface utilisateur en préversion](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Au cours de la mise à niveau de hello, nom du nœud de premier hello désigne hello machine de hello. 
3. Maintenant, ajoutez un nœud. Bonjour **passerelle** , cliquez sur **ajouter un nœud**.  

    ![Passerelle de gestion des données - Menu Ajouter un nœud](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Suivez les instructions de hello précédente section tooset nœud de hello. 

### <a name="installation-best-practices"></a>Bonnes pratiques d’installation

- Configurer le mode d’alimentation sur l’ordinateur hôte de hello pour la passerelle de hello afin que hello machine ne pas en veille prolongée. Si l’ordinateur hôte de hello en veille prolongée, passerelle de hello ne répond pas les demandes toodata.
- Sauvegardez le certificat hello associé hello passerelle.
- Vérifiez que la configuration de tous les nœuds est similaire pour atteindre les performances idéales (recommandé). 
- Ajoutez une disponibilité élevée tooensure au moins deux nœuds.  

### <a name="tlsssl-certificate-requirements"></a>Configuration requise des certificats TLS/SSL
Voici les exigences hello pour certificat TLS/SSL hello qui est utilisé pour sécuriser les communications entre les nœuds de la passerelle :

- certificat de Hello doit être un X509 approuvée publiquement certificat v3.
- Tous les nœuds de passerelle doivent approuver ce certificat. 
- Nous vous recommandons d’utiliser des certificats émis par une autorité de certification (tierce) publique.
- Prise en charge de toutes les tailles de clé prises en charge par Windows Server 2012 R2 pour les certificats SSL.
- Non-prise en charge des certificats qui utilisent des clés CNG.
- Les certificats utilisant des caractères génériques sont pris en charge. 


## <a name="monitor-a-multi-node-gateway"></a>Surveiller une passerelle à plusieurs nœuds
### <a name="multi-node-gateway-monitoring"></a>Surveillance d’une passerelle à plusieurs nœuds
Bonjour portail Azure, vous pouvez afficher l’instantané quasiment en temps réel de l’utilisation des ressources (processeur, mémoire, network(in/out), etc.) sur chaque nœud, ainsi que les États des nœuds de la passerelle. 

![Passerelle de gestion des données - Surveillance de plusieurs nœuds](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

Vous pouvez activer **paramètres avancés** Bonjour **passerelle** toosee avancé des métriques telles que la page **réseau**(entrée/sortie), **rôle et l’état d’informations d’identification**, qui est utile pour résoudre les problèmes de passerelle, et **travaux simultanés** (en cours d’exécution / limite) qui peut être modifié / modifié en conséquence lors de l’optimisation des performances. Hello tableau suivant fournit des descriptions des colonnes Bonjour **passerelle nœuds** liste :  

Propriété de surveillance | Description
:------------------ | :---------- 
Nom | Nom de la passerelle de logique de hello et les nœuds associés hello passerelle.  
État | État de la passerelle de logique de hello et les nœuds de passerelle hello. Exemple : En ligne/Hors connexion/Limité/etc. Pour plus d’informations sur ces états, consultez la section [État de la passerelle](#gateway-status). 
Version | Affiche la version hello de passerelle de logique hello et chaque nœud de passerelle. version Hello de passerelle de logique hello est déterminée en fonction de la version de la majorité des nœuds dans le groupe de hello. S’il existe des nœuds avec différentes versions dans le programme d’installation de la passerelle logique hello, seuls les nœuds hello avec hello même numéro de version en tant que fonction de passerelle logique hello correctement. D’autres sont en mode limité de hello et doivent toobe mis à jour manuellement (uniquement au cas où la mise à jour automatique échoue). 
Mémoire disponible | Mémoire disponible sur un nœud de passerelle. Cette valeur est un instantané en quasi temps réel. 
Utilisation du processeur | Utilisation du processeur d’un nœud de passerelle. Cette valeur est un instantané en quasi temps réel. 
Réseau (entrée/sortie) | Utilisation du réseau d’un nœud de passerelle. Cette valeur est un instantané en quasi temps réel. 
Tâches simultanées (en cours d’exécution/limite) | Nombre de travaux ou tâches qui s’exécutent sur chaque nœud. Cette valeur est un instantané en quasi temps réel. Limite signifie travaux simultanés de hello maximal pour chaque nœud. Cette valeur est définie en fonction de la taille de la machine hello. Vous pouvez augmenter tooscale de limite hello de l’exécution de travaux simultanés dans les scénarios avancés, où processeur / mémoire / réseau est sous-utilisée, mais les activités dépassent ce délai. Cette fonctionnalité est également disponible avec une passerelle à un seul nœud (même quand la fonctionnalité de l’évolutivité et disponibilité hello n’est pas activée). Pour plus d’informations, consultez la section [Considérations d’échelle](#scale-considerations). 
Rôle | Il existe deux types de rôles : répartiteur et rôle de travail. Tous les nœuds sont employés, ce qui signifie qu’ils peuvent tous être utilisés tooexecute travaux. Il n'existe qu’un seul nœud de répartiteur, ce qui est utilisé toopull tâches/tâches à partir des services de cloud computing et les distribuer des nœuds de travail toodifferent (y compris lui-même). 

![Passerelle de gestion des données - Surveillance avancée de plusieurs nœuds](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>État de la passerelle

Hello tableau suivant fournit les états possibles d’un **nœud passerelle**: 

État  | Commentaires/Scénarios
:------- | :------------------
En ligne | Nœud connecté service de fabrique tooData.
Hors ligne | Le nœud est hors connexion.
Mise à niveau | nœud de Hello est en cours de la mise à jour automatique.
Limité | En raison du problème de tooConnectivity. Peut être dû à problème de port 8050 tooHTTP, problème de connectivité de bus de service ou un problème de synchronisation d’informations d’identification. 
Inactif | Nœud est dans une configuration différente de la configuration hello d’autres nœuds majoritaire.<br/><br/> Un nœud peut être inactif lorsqu’il ne peut pas se connecter à des nœuds de tooother. 


Hello tableau suivant fournit les états possibles d’un **passerelle logique**. état de la passerelle Hello dépend des États des nœuds de passerelle hello. 

État | Commentaires
:----- | :-------
Doit être inscrite | Aucun nœud n’est encore inscrit toothis logique passerelle
En ligne | Les nœuds de passerelle sont en ligne.
Hors ligne | Aucun nœud n’est en ligne.
Limité | Tous les nœuds inclus dans cette passerelle ne sont pas dans un état intègre. Cet état est un avertissement pouvant indiquer que certains nœuds sont en panne ! <br/><br/>Peut être dû à problème de synchronisation toocredential sur le nœud de répartiteur/de travail. 

### <a name="pipeline-activities-monitoring"></a>Surveillance de pipeline/des activités
Hello portail Azure fournit un expérience avec les détails au niveau du nœud granulaire de surveillance de pipeline. Par exemple, il indique quelles activités se sont exécutées sur quel nœud. Ces informations peuvent être utiles pour comprendre les problèmes de performances sur un nœud particulier, par exemple en raison de la limitation de toonetwork. 

![Passerelle de gestion des données - Surveillance de plusieurs nœuds pour les pipelines](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![Passerelle de gestion des données - Détails de pipeline](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>Considérations d’échelle

### <a name="scale-out"></a>Montée en charge
Hello lorsque **mémoire disponible est faible** et hello **l’utilisation du processeur est élevée**, ajoutez un nouveau nœud permet de montée en puissance parallèle hello charge sur plusieurs ordinateurs. Si des activités échouent en raison de nœud tootime-out ou la passerelle est hors connexion, il est utile si vous ajoutez une passerelle toohello de nœud.
 
### <a name="scale-up"></a>Monter en puissance
Lorsque la mémoire disponible hello et processeur ne sont pas utilisées correctement, mais capacité d’inactivité hello est de 0, vous devez mettre à l’échelle vers le haut en augmentant le nombre de hello de travaux simultanés pouvant s’exécuter sur un nœud. Vous pouvez également tooscale haut lorsque les activités dépassent ce délai, car la passerelle de hello est surchargé. Comme indiqué dans hello suivant l’image, vous pouvez augmenter la capacité maximale de hello pour un nœud. Nous vous suggérons doublant toostart avec.  

![Passerelle de gestion des données - Considérations d’échelle](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>Problèmes connus/nouveautés

- Actuellement, vous pouvez avoir des nœuds de passerelle physique toofour pour une passerelle logique unique. Si vous avez besoin de plus de quatre nœuds pour des raisons de performances, envoyer un courrier électronique trop[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com).
- Vous ne peut pas réenregistrer un nœud de passerelle avec la clé d’authentification hello à partir d’un autre tooswitch passerelle logique à partir de la passerelle de logique actuelle hello. dans le Registre toore, désinstaller hello passerelle nœud de hello, réinstallez hello passerelle et l’enregistrer avec la clé d’authentification hello pour hello autres passerelle logique. 
- Si le proxy HTTP est requis pour tous les nœuds de votre passerelle, la définition de proxy de hello dans diahost.exe.config et diawp.exe.config et utiliser hello server manager toomake que tous les nœuds ont hello même diahost.exe.config et diawip.exe.config. Consultez la section [Configurer les paramètres du proxy](data-factory-data-management-gateway.md#configure-proxy-server-settings) pour plus d’informations. 
- toochange en mode de chiffrement pour la communication de nœud à l’autre dans le Gestionnaire de Configuration de passerelle, supprimez tous les nœuds de hello dans portail hello sauf un. Ajoutez ensuite les nœuds après la modification du mode de chiffrement hello.
- Utiliser un certificat SSL officiel si vous choisissez le canal de communication de nœud à nœud tooencrypt hello. Certificat auto-signé peut entraîner des problèmes de connectivité comme hello même certificat ne peut pas être approuvé dans la liste des autorités de certification sur d’autres ordinateurs. 
- Impossible d’inscrire une passerelle nœud tooa logique lors de la version du nœud hello est inférieure à la version de la passerelle logique hello. Supprimez tous les nœuds de passerelle de logique hello portail afin que vous pouvez inscrire un node(downgrade) version inférieure il. Si vous supprimez tous les nœuds d’une passerelle logique, installer et enregistrer manuellement nouvelle passerelle logique toothat de nœuds. L’installation rapide n’est pas prise en charge dans ce cas.
- Vous ne pouvez pas utiliser le programme d’installation express tooinstall nœuds tooan logique passerelle existante, qui utilise toujours les informations d’identification du cloud. Vous pouvez vérifier où les informations d’identification de hello sont stockées à partir de hello Gestionnaire de Configuration de passerelle sur l’onglet Paramètres de hello.
- Vous ne pouvez pas utiliser le programme d’installation express tooinstall nœuds tooan logique passerelle existante, qui a le chiffrement de nœud à l’autre est activé. Comme paramètre de mode de chiffrement hello implique l’ajout manuel des certificats, installation express n’est pas plus d’une option. 
- Pour effectuer une copie de fichiers à partir d’un environnement local, vous ne devez plus utiliser \\localhost ni C:\fichiers car localhost ou le lecteur local ne sont peut-être pas accessibles par le biais de tous les nœuds. Au lieu de cela, utilisez \\emplacement des fichiers ServerName\files toospecify.


## <a name="rolling-back-from-hello-preview"></a>Restauration de la version préliminaire de hello 
tooroll à partir de la version préliminaire de hello, supprimez tous les nœuds, mais un seul nœud. Peu importe quels nœuds vous supprimer, mais assurez-vous de qu'avoir au moins un nœud dans la passerelle de logique hello. Vous pouvez supprimer un nœud en désinstallant la passerelle sur l’ordinateur de hello ou à l’aide de hello portail Azure. Bonjour portail Azure, Bonjour **Data Factory** , cliquez sur hello de toolaunch services lié **services liés** page. Hello de hello sélectionnez passerelle toolaunch **passerelle** page. Dans la page de la passerelle hello, vous pouvez voir les nœuds hello associés hello passerelle. page de Hello vous permet de supprimer un nœud à partir de la passerelle de hello.
 
Après la suppression, cliquez sur **fonctionnalités en version préliminaire** hello même page du portail Azure et désactiver la fonctionnalité d’aperçu hello. Vous avez réinitialisé votre passerelle tooone nœud GA (disponibilité générale).


## <a name="next-steps"></a>Étapes suivantes
Passez en revue hello suivant des articles :
- [Passerelle de gestion des données](data-factory-data-management-gateway.md) -fournit une vue d’ensemble détaillée de la passerelle de hello.
- [Déplacer des données entre des magasins de données locaux et dans le cloud](data-factory-move-data-between-onprem-and-cloud.md) - contient une procédure pas à pas donnant des instructions sur l’utilisation d’une passerelle à nœud unique. 
