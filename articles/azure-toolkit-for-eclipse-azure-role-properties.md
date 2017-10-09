---
title: "Propriétés du rôle d’aaaAzure"
description: "Découvrez comment toouse hello boîte à outils Azure pour les paramètres de rôle Azure tooconfigure Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Propriétés du rôle Azure
Peuvent être définir divers paramètres de configuration pour votre rôle Azure hello boîte à outils Azure pour Eclipse.

## <a name="configuring-azure-role-properties"></a>Configuration des propriétés de rôle Azure
Configuration des propriétés de votre rôle Azure s’effectue via les boîtes de dialogue propriété hello pour votre rôle de travail. Menu contextuel Ouvrir hello rôle de hello dans le volet de l’Explorateur de projets d’Eclipse et les sélectionner hello **Azure** sous-menu. (Si vous ne voyez pas rôle hello Bonjour Explorateur de projets Eclipse, développez votre projet Azure dans l’Explorateur de projets.)

![][ic789599]

Hello diverses propriétés qui peuvent être définies à partir de hello **propriétés** les boîtes de dialogue sont décrites dans cette rubrique. Notez que de nombreuses propriétés sont renseignées automatiquement lorsque vous créez un projet de déploiement Azure.

Hello suivant des pages de propriétés est disponible pour les rôles Azure.

* [Propriétés de machine virtuelle](#virtual_machine_properties)
* [Propriétés de mise en cache](#caching_properties)
* [Propriétés de certificats](#certificates_properties)
* [Propriétés des composants](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Propriétés des points de terminaison](#endpoints_properties)
* [Propriétés des variables d’environnement](#environment_variables_properties)
* [Propriétés d’équilibre de charge/affinité de session (appelées « sessions temporaires »)](#session_affinity_properties)
* [Propriétés du stockage local](#local_storage_properties)
* [Propriétés de configuration de serveur](#server_configuration_properties)
* [Propriétés de déchargement SSL](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Propriétés de machine virtuelle
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **propriétés**, et vous avez taille de machine virtuelle hello capacité toochange hello et également modifier nombre de Hello d’instances, comme indiqué dans hello suivant l’image.

![][ic719499]

> [!NOTE]
> Windows uniquement : lorsque vous définissez hello nombre d’instances tooa valeur supérieure à 1 et que vous configurez également un serveur d’applications, hello toolkit permet uniquement 1 toorun d’instance de rôle dans l’émulateur hello, indépendamment de ce paramètre. Il s’agit des conflits de liaison de port tooavoid entre hello différentes instances de serveur (par exemple, tous les lors de la tentative toobind tooport 8080) lorsqu’ils s’exécutent sur hello même ordinateur. Définir le nombre d’instances de souhaitée est conservé, mais il prend effet uniquement lorsque vous déployez toohello cloud.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Propriétés de mise en cache
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **mise en cache**. Cette boîte de dialogue, vous pouvez activer des caches compatible avec memcache colocalisés nommés, ce qui permet de vitesse de toohelp vos applications web.

![][ic719483]

Au sein de hello **mise en cache** page de propriétés, vous pouvez spécifier les paramètres globaux pour hello suivant :

* indique si la mise en cache colocalisée est activée ou non.
* taille du cache de Hello sous forme de pourcentage de mémoire.
* nom du compte de stockage Hello pour enregistrer l’état du cache hello lorsque votre application s’exécute comme un service cloud, ou aucun si vous ne souhaitez pas l’état de cache toosave hello. (nom de compte de stockage hello n’est pas utilisé lorsque vous exécutez votre application dans l’émulateur de calcul hello.) Si vous définissez les nom de compte de stockage hello trop**(auto)** (qui est par défaut de hello), votre configuration de mise en cache utilise automatiquement hello même compte de stockage que celui que vous sélectionnez Bonjour hello **publier tooAzure**boîte de dialogue.

> [!NOTE]
> Hello **(auto)** paramètre aura d’effet hello ne souhaité que si vous publiez votre déploiement à l’aide de hello boîte à outils Eclipse Assistant de publication. Si à la place vous publiez le fichier .cspkg de hello manuellement à l’aide d’un mécanisme externe, par exemple hello [portail de gestion Azure][Azure Management Portal], déploiement de hello ne fonctionnera pas correctement.
> 
> 

Hello suivant la boîte de dialogue affiche les propriétés de hello pour un cache.

![][ic719501]

* **Nom :** nom hello Hello colocalisés du cache.
* **Numéro de port :** hello toouse numéro de port pour le cache de hello.
* **Stratégie d’expiration :** d'entre hello valeurs suivantes qui spécifie quand une clé dans le cache de hello expire.
  * **Absolue :** clé de hello expire lorsque hello délai spécifié par **Minutes toolive** est atteinte.
  * **N’expire jamais :** clé de hello n’a pas de délai d’expiration.
  * **Fenêtre défilante :** clé de hello expire si elle n’a pas été accédé pour la quantité de hello de temps spécifié par **Minutes toolive**; chaque fois qu’il est accessible, réinitialisation de l’horloge d’expiration hello.
* **Minutes toolive :** nombre maximal de minutes de vie d’une clé toolive, toohello d’expiration de l’objet.
* **Haute disponibilité avec sauvegardes répliquées sur des instances de rôle différentes :** si cette option est activée, elle offre la haute disponibilité en utilisant des sauvegardes répliquées sur différentes instances de rôle. Notez qu’au moins deux instances de rôle doit être en vigueur pour votre déploiement pour toowork de cette fonctionnalité.

tooadd un nouveau cache, cliquez sur hello **ajouter** bouton Bonjour **mise en cache** page de propriétés et un **configurer un Cache nommé** boîte de dialogue s’ouvre. Fournir des valeurs pour les propriétés hello décrites ci-dessus.

toomodify un cache nommé, sélectionnez hello cache et cliquez sur hello **modifier** bouton Bonjour **mise en cache** page de propriétés. Une boîte de dialogue s’ouvre, permettant ainsi vous toomodify hello propriétés du cache. Appuyez sur **OK** valeurs de cache toosave hello.

toodelete un cache, sélectionnez hello cache et cliquez sur hello **supprimer** bouton Bonjour **mise en cache** page de propriétés, puis cliquez sur **Oui** suppression de hello tooconfirm.

Pour plus d’informations sur la façon de toouse mise en cache, consultez [comment tooUse colocalisés mise en cache][How tooUse Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Propriétés de certificats
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **certificats**.

![][ic710964]

Dans cette boîte de dialogue, vous pouvez ajouter ou supprimer des certificats référencés par votre projet Eclipse. Notez que les certificats hello répertoriés ici ne sont pas automatiquement stockés dans un keystore Java et par conséquent, ne sont pas automatiquement disponibles pour une utilisation à partir d’une application Java. Ils sont uniquement inscrits avec Azure afin que leur préchargement dans hello Windows certificat stocker sur des machines virtuelles de hello votre déploiement en cours d’exécution et est ensuite utilisé par d’autres logiciels Windows. Actuellement, hello uniquement la fonctionnalité de boîte à outils hello qui utilise des certificats de hello référencés dans hello **certificats** boîte de dialogue est [déchargement SSL][SSL Offloading], en raison de tooits dépendance envers les Internet Information Services (IIS) et l’Application Request Routing (ARR), qui nécessitent hello toobe de certificat approprié mis à disposition de cette manière.

Lorsque vous déployez votre tooAzure de projet à l’aide d’Assistant de publication hello, vous seront demandée toopoint à hello PFX Personal Information Exchange () fichiers certificats toothese, ainsi que leurs mots de passe correspondants dans l’ordre tooautomatically les télécharger toohello Service Azure, mais uniquement si elles n'ont pas été téléchargés précédemment.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Propriétés des composants
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **composants**. Cette boîte de dialogue, vous avez hello capacité tooadd, modifiez, ou supprimez des composants de votre rôle hello, ainsi que de modifiez commande hello dans lequel ils sont traités.

![][ic719502]

fonctionnalité des composants Hello vous permet de projet déploiement Azure tooyour tooadd dépendances, telles que les projets d’application Java, les fichiers spéciaux et les instructions exécutables de ligne de commande qui sont requises par votre déploiement.

Pour chaque composant, vous pouvez spécifier :

* Hello étape toobe est effectuée lors de l’importation de composant de hello dans votre projet de déploiement Azure lorsqu’elle est générée.
* Hello toobe d’étape effectuée lors du déploiement de ce composant Bonjour cloud Azure.

> [!NOTE]
> Lorsque vous spécifiez les fichiers de composant ou des lignes de commande, gardez à l’esprit que votre déploiement sera publié tooa machine virtuelle Windows vos étapes personnalisées doivent donc être valides pour un système d’exploitation Windows. 
> 
> 

Composants ont hello propriétés suivantes :

* **Importation :** méthode qui indique comment le composant de hello est importé dans le projet de hello lors de la génération du projet hello. Cela peut être une des valeurs suivantes de hello :
  * **copie :** composant de hello est copié à partir du chemin d’accès local hello spécifié par hello **de** propriété du rôle hello **approot** active.
  * **EAR :** composant de hello est une archive d’entreprise (EAR) Java importée à partir d’un projet d’Application Enterprise au chemin d’accès local hello spécifié par hello **de** propriété. (Cela est détecté automatiquement par selon la nature hello du projet hello à cet emplacement de la boîte à outils hello).
  * **JAR :** composant de hello est une archive Java (JAR) et est importée à partir d’un projet Java dans le chemin d’accès local hello spécifié par hello **de** propriété. (Cela est détecté automatiquement par selon la nature hello du projet hello à cet emplacement de la boîte à outils hello).
  * **none :** aucune action n’est effectuée de composant de hello tooimport. Cela s’applique lorsque le composant de hello est supposé tooalready être présents dans le rôle hello **approot** active, ou lorsque le composant de hello est simplement une instruction exécutable de ligne de commande, comme spécifié dans hello **comme**propriété lorsque hello **déployer** méthode est **exec**.
  * **WAR :** composant Windows hello est une archive d’application web Java (WAR) et qu’il est importé à partir d’un projet Web dynamique au niveau du chemin d’accès local hello spécifié par hello **de** propriété. (Cela est détecté automatiquement par selon la nature hello du projet hello à cet emplacement de la boîte à outils hello).
  * **ZIP :** composant Windows hello est un fichier zip et qu’il est importé par le fichier ou répertoire de hello zip spécifié par hello **de** propriété.
* **À partir de :** chemin d’accès Source sur votre dossier de toohello ordinateur local ou d’un fichier qui représente le déploiement de tooyour tooimport hello ou les éléments. Les variables d’environnement Windows peuvent être utilisées dans cette propriété. Tous les composants importables seront importées dans du rôle hello **approot** active lors de la génération du projet hello.
  
    Notez que vous avez hello capacité toodeploy un composant à partir d’un téléchargement lors du déploiement toohello cloud (pas un émulateur de calcul hello). Consultez les informations connexes ci-dessous concernant l’ajout d’un composant.    
* **En tant que :** nom de fichier sous le hello composant sera importé dans du rôle hello **approot** répertoire, puis déployé dans hello cloud Azure. Laissez cette tookeep vide propriété hello hello nom tel qu’il est sur l’ordinateur local de hello. (Pour des composants exécutables, c'est-à-dire celles dont **déployer** méthode est définie trop**exec**, cela peut être une instruction de ligne de commande Windows arbitraire.)
  
  > [!IMPORTANT]
  > Si vous utilisez des caractères d’espace pour cette valeur, elles sont gérées différemment en fonction de hello méthode de déploiement. Si la méthode de déploiement hello est **exec**, espaces sont considérées comme des séparateurs d’arguments de ligne de commande et non comme faisant partie du nom de fichier hello. Déployer des méthodes pour tous les autres, les espaces sont considérées comme faisant partie du nom de fichier hello.
  > 
  > 
* **Déployer :** méthode indiquant hello action appliquée toohello composant lorsque hello déploiement est démarré. Cela peut être une des valeurs suivantes de hello :
  
  * **copie :** composant de hello est copié toohello chemin de destination spécifié par hello **à** propriété.
  * **EXEC :** composant de hello est une instruction exécutable de ligne de commande Windows exécutée dans le contexte de hello du chemin d’accès hello spécifié par hello **à** propriété, au moment de hello hello déploiement démarre.
  * **none :** aucune action n’est appliqué toohello composant lorsque le déploiement de hello commence.
  * **ZIP :** composant de hello est décompressé toohello chemin de destination spécifié par hello **à** propriété. Cette méthode est disponible uniquement lorsque hello **importation** propriété **zip**.
* **À :** chemin d’accès de Destination sur l’ordinateur virtuel de hello où hello composant ne sera déployé. Variables d’environnement Windows peuvent être utilisées dans cette propriété, et les chemins d’accès sont trop relatives**approot**.

tooadd un nouveau composant, cliquez sur hello **ajouter** bouton Bonjour **composants** page de propriétés et un **composant de rôle Azure** boîte de dialogue s’ouvre. Fournir des valeurs pour les propriétés hello décrites ci-dessus. 

Hello Voici un exemple d’ajout d’un nouveau composant WAR.

![][ic719503]

Lorsque la déploiement toohello cloud (pas émulateur de calcul hello), si vous souhaitez que le composant de hello toodeploy à partir d’un téléchargement, assurez-vous que **dans le cloud, au lieu d’inclure dans le package de hello, déployer à partir de** est activée. Si vous souhaitez toodownload à partir de votre compte de stockage Azure, sélectionnez le compte de stockage hello dans hello **compte de stockage** liste déroulante (vous pouvez cliquer sur hello **comptes** lien toomodify Nouveautés dans la liste de hello), action renseigne partiellement Bonjour **URL** champ, puis renseignez hello portion restante de l’URL de hello. Si vous ne souhaitez pas toouse le stockage Azure, sélectionnez **(aucun)** de hello **compte de stockage** déroulante liste, puis entrez les composants de tooyour URL hello Bonjour **URL** champ. Spécifiez l’une des méthodes suivantes de hello :

* **copie :** composant de téléchargement hello est copié toohello chemin de destination spécifié par hello **tooDirectory** chemin d’accès.
* **même :** hello même méthode utilisée pour **déployer à partir de téléchargement** pour **déployer à partir du package**.
* **ZIP :** composant de hello téléchargé est décompressé toohello chemin de destination spécifié par hello **tooDirectory** chemin d’accès.

toomodify un hello du composant et cliquez sur composant, sélectionnez hello **modifier** bouton Bonjour **composants** page de propriétés. Une boîte de dialogue s’ouvre, permettant ainsi vous toomodify hello les propriétés du composant. Appuyez sur **OK** valeurs de composant toosave hello.

toodelete un hello du composant et cliquez sur composant, sélectionnez hello **supprimer** bouton Bonjour **composants** page de propriétés, puis cliquez sur **Oui** suppression de hello tooconfirm.

Les composants sont traités dans l’ordre de hello. Hello d’utilisation **monter** et **Descendre** boutons de commande de hello tooarrange.

> [!NOTE]
> fonctionnalité de configuration de serveur Hello s’appuie également sur des composants. Ces composants ne peut pas être supprimés ou modifiés sans supprimer la configuration du serveur hello correspondant. Vous êtes invité à ce sujet lors de la tentative de toomake modifications toosuch composants.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Propriétés des points de terminaison
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **points de terminaison**. Cette boîte de dialogue ont hello capacité toocreate un point de terminaison, ainsi que modifier ou supprimer un point de terminaison, comme indiqué dans hello suivant l’image.

![][ic719505]

tooadd un point de terminaison, cliquez sur hello **ajouter** bouton Bonjour **points de terminaison** page de propriétés et un **ajouter le point de terminaison** boîte de dialogue s’ouvre.

![][ic710897]

Entrez un nom pour le point de terminaison hello, sélectionnez le type de hello (soit **entrée**, **interne**, ou **InstanceInput**), puis spécifiez le port public et privé de hello. Appuyez sur **OK** toosave hello nouvelles valeurs de point de terminaison.

En fonction de type hello du point de terminaison, vous pouvez utiliser des plages de ports comme suit :

* Pour un point de terminaison d’instance d’entrée, port public de hello peut être une plage de ports (par exemple **2000-2010**) et un port privé hello est une valeur fixe.
* Pour un point de terminaison interne, port public de hello n’est pas utilisé et un port privé hello peut être une plage, ou un vide ou un jeu tooan astérisque tooindicate qu’il est défini automatiquement par Azure.
* Pour les points de terminaison d’entrée, port public de hello peut être uniquement une valeur fixe, et un port privé hello peut être une valeur fixe, ou un vide ou un jeu tooan astérisque tooindicate qu’il est défini automatiquement par Azure.

Si vous voulez toouse un numéro de port unique au lieu d’une plage, laissez une zone de texte hello fin hello de plage de hello vide.

Pour les ports qui sont tooautomatic de jeu, si vous avez besoin de toodetermine le port réellement utilisé pendant l’exécution, votre application peut utiliser hello API Azure Service Runtime, qui est décrit dans hello [com.microsoft.windowsazure.serviceruntime package Résumé][com.microsoft.windowsazure.serviceruntime package summary].

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

toomodify un point de terminaison, sélectionnez le point de terminaison hello et cliquez sur hello **modifier** bouton Bonjour **points de terminaison** page de propriétés. Une boîte de dialogue s’ouvre, ce qui vous permet de ports publics et privés, type et nom de point de terminaison toomodify hello. Appuyez sur **OK** toosave hello modifié les valeurs de point de terminaison.

toodelete un point de terminaison, sélectionnez le point de terminaison hello et cliquez sur hello **supprimer** bouton Bonjour **points de terminaison** page de propriétés, puis cliquez sur **Oui** suppression de hello tooconfirm.

Dans l’ordre tooproperly configurer certaines fonctionnalités hello (par exemple, le déchargement SSL, l’affinité de Session ou la mise en cache) activée par l’utilisateur hello sur un rôle, boîte à outils hello peut configurer automatiquement des points de terminaison spéciaux qui sont répertoriés, ainsi que les points de terminaison définis par l’utilisateur. Hello toolkit empêche l’utilisateur de hello de modifier ou supprimer ces points de terminaison générés automatiquement tant que hello associé la fonctionnalité est activée.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Propriétés des variables d’environnement
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **Variables d’environnement**. Cette boîte de dialogue ont hello capacité toocreate une variable d’environnement, ainsi que modifier ou supprimer une variable d’environnement, comme indiqué dans hello suivant l’image.

![][ic719506]

Variables d’environnement sont script de démarrage tooyour disponible au démarrage de rôle de hello.

> [!NOTE]
> Lorsque vous spécifiez des variables d’environnement, gardez à l’esprit que votre déploiement sera publié tooa machine virtuelle Windows vos variables d’environnement doivent être valides pour un système d’exploitation Windows.
> 
> 

Comme exemple d’une variable d’environnement qui est disponible au démarrage de rôle de hello, créez une variable d’environnement en cliquant sur hello **ajouter** bouton. Hello suivant montre une variable d’environnement nommée **MyRoleVersion** et l’attribution valeur de hello **1.0**.

![][ic659268]

Dans votre code jsp, vous pouvez afficher la valeur hello à l’aide de hello `System.getenv` méthode :

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Résultat de cette sortie lors de l’exécution de votre application :

![][ic552233]

toomodify une variable d’environnement, sélectionnez la variable d’environnement hello et cliquez sur hello **modifier** bouton Bonjour **Variables d’environnement** page de propriétés. Une boîte de dialogue s’ouvre, permettant ainsi vous toomodify hello variable propriétés d’environnement. Appuyez sur **OK** valeurs de variable d’environnement toosave hello.

toodelete une variable d’environnement, sélectionnez la variable d’environnement hello et cliquez sur hello **supprimer** bouton Bonjour **Variables d’environnement** page de propriétés, puis cliquez sur **Oui**suppression de hello tooconfirm.

Dans l’ordre tooproperly configurer certaines fonctionnalités hello (par exemple, la Configuration du serveur, le débogage à distance ou de stockage Local) activée par l’utilisateur hello sur un rôle, boîte à outils hello peut configurer automatiquement les variables d’environnement spéciales qui sont répertoriés avec variables d’environnement définie par l’utilisateur. Hello toolkit empêche l’utilisateur de hello de modifier ou supprimer ces variables d’environnement générées automatiquement tant que hello associé la fonctionnalité est activée.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Propriétés d’équilibre de charge/affinité de session (appelées « sessions temporaires »)
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **l’équilibrage de charge**. Cette boîte de dialogue vous hello capacité tooenable ou désactivez l’affinité de session, comme indiqué dans hello suivant l’image.

![][ic719492]

Pour plus d’informations, consultez [Affinité de session][Session Affinity]. Notez également le comportement de cette fonctionnalité dans le contexte de hello de déchargement SSL, comme décrit dans [déchargement SSL][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Propriétés du stockage local
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **stockage Local**. Cette boîte de dialogue ont hello capacité toocreate, modifier ou supprimer un stockage local temporaire pour l’ordinateur virtuel hello qui exécute votre application. Des valeurs spécifiques peuvent être définies pour la taille de hello du stockage local de hello, ainsi que si le contenu de hello est conservés lors de la hello rôle est recyclé, comme indiqué dans hello suivant l’image.

![][ic719508]

Vous pouvez spécifier une variable d’environnement qui correspond le stockage local de toohello.

Par défaut, tous les éléments que vous déployez dans Azure sont placé (et décompressé) Bonjour **approot** dossier d’instance de rôle hello. Alors que la plupart des déploiements simples peuvent y tenir même après décompression, espace hello alloué hello **approot** répertoire est limité et pas bien défini (moins de 1 Go est une règle empirique raisonnable). Par conséquent, tooensure Azure alloue suffisamment d’espace disque pour les déploiements plus importants qui ne répondent pas à Bonjour **approot** dossier, vous devez définir une ressource de stockage local à l’aide de hello **stockage Local** boîte de dialogue. Pour un moyen simple de toodo, consultez [déploiements à grande échelle déploiement][Deploying Large Deployments].

Vous pouvez aisément référencer la ressource de stockage hello à partir de scripts de démarrage (par exemple, votre **startup.cmd**) à l’aide de la variable d’environnement hello automatiquement associé à la boîte à outils Eclipse de hello hello ressource comme indiqué dans hello  **Stockage local** boîte de dialogue. Cette variable d’environnement contient le chemin d’accès complet de hello de ressource locale de hello que vous avez configuré au moment de hello que votre script de démarrage est exécutée. 

toomodify une ressource de stockage local, sélectionnez la ressource de stockage local hello et cliquez sur hello **modifier** bouton Bonjour **stockage Local** page de propriétés. Une boîte de dialogue s’ouvre, permettant ainsi vous toomodify hello stockage local des propriétés de ressource. Appuyez sur **OK** valeurs de ressources de stockage local toosave hello.

toodelete une ressource de stockage local, sélectionnez la ressource de stockage local hello et cliquez sur hello **supprimer** bouton Bonjour **stockage Local** page de propriétés, puis cliquez sur **Oui** suppression de hello tooconfirm.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Propriétés de configuration de serveur
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **Configuration du serveur**. Cette boîte de dialogue, vous avez hello capacité tooadd, supprimer et de modifier hello JDK et serveur d’applications Java utilisé par votre déploiement, ainsi que d’ajouter ou de supprimer des applications hello (tels que les fichiers WAR, JAR ou EAR) utilisées par votre déploiement.

### <a name="jdk-configuration"></a>Configuration JDK
Cette boîte de dialogue vous permet de toospecify hello JDK package toouse pour votre déploiement. Si vous utilisez Eclipse sur Windows, vous pouvez spécifier hello JDK package toouse localement lors de l’exécution dans hello émulateur Azure et que vous disposez hello option toodeploy que tooAzure installation locale. Sur les systèmes d’exploitation non-Windows, paramètre hello d’émulateur JDK n’est pas applicable et vous ne pouvez pas déployer hello localement installé JDK, car il n’est pas compatible avec Windows. Toutefois, quel que soit hello système d’exploitation que vous utilisez, vous pouvez toujours choisir parmi hello 3e partie JDK packages toodeploy tooAzure, ou pointer sur votre propre package JDK compatible Windows à partir d’un autre emplacement de téléchargement.

Hello Voici un exemple de comment vous pouvez spécifier un JDK sur Windows :

![][ic780647]

Si vous utilisez Eclipse sur Windows, vous pouvez spécifier un toouse JDK avec hello compute emulator ; toodo, veillez à **hello utilisez JDK à partir de ce chemin d’accès de fichier pour tester localement** est archivé hello **déploiement d’émulateur** section. Ensuite, spécifiez le chemin d’accès local de hello tooyour JDK ; Vous pouvez parcourir toodifferent JDK si hello celui que vous voulez toouse n’est pas sélectionné automatiquement. Vous avez également hello option toodeploy votre tooyour JDK service cloud Azure ; toodo, sélectionnez hello **déployer mon JDK local (stockage toocloud de chargement automatique)** option Bonjour **déploiement de cloud computing** section.

Remarque : Sur les systèmes d’exploitation non-Windows, hello **déploiement d’émulateur** paramètres et hello **déployer mon JDK local** option ne sont pas disponibles. Hello exemple suivant illustre la spécification d’un JDK sur un Mac ou autres pris en charge le système d’exploitation non Windows :

![][ic789643]

Quel que soit le système d’exploitation du hello vous utilisez, vous avez hello suivant deux **déploiement de cloud computing** options pour la source de hello et le type de votre package JDK :

* **Déployer un package JDK tiers disponible Azure** 
* **Déploiement depuis un téléchargement personnalisé** 

Si vous utilisez hello **déployer un package JDK tiers 3e à partir d’Azure** option :

1. Activez hello case **déployer un package JDK tiers 3e à partir d’Azure**.
2. Dans la liste déroulante hello, sélectionnez hello 3e package JDK tiers disponible sur Azure.
3. Votre **JDK** onglet recherche similaire suivant toohello sur Windows : ![][ic780648] et il ressemblera similaire suivant toohello sur Mac OS ou autre prise en charge des systèmes d’exploitation non Windows :![][ic789643]
4. Cliquez sur **OK** toosave vos modifications.
5. Lorsque tooaccept demandée hello contrat de licence de fournisseur de package hello 3e partie JDK, passez en revue les termes du contrat de licence hello. Si vous acceptez les termes du contrat de hello, cliquez sur **Oui** tooclose hello **accepter le contrat de licence** boîte de dialogue.
    Notez que hello sous-jacent logique pour lequel les éléments apparaissent dans la liste déroulante de hello pour hello **déployer un package JDK tiers 3e à partir d’Azure** option peut être personnalisée. éléments de hello toocustomize, Bonjour **JDK** boîte de dialogue, cliquez sur hello **personnaliser** lien. Cela entraînera la fermeture hello **JDK** page de propriétés et ouvrez hello **componentsets.xml** fichier dans Eclipse, que vous pouvez modifier en fonction des besoins. Documentation de **componentsets.xml** est inclus dans hello **componentsets.xml** fichier lui-même.

Si vous utilisez hello **déployer un JDK à partir d’un téléchargement personnalisé** option :

1. Créer un fichier ZIP de votre répertoire d’installation de JDK, ce nœud de répertoire hello lui-même est enfant hello de structure de hello ZIP et non son contenu. Prenez note du nom hello du répertoire de hello, que vous serez besoin ultérieurement, gardez à l’esprit ce JDK installation sera tooa déployé l’ordinateur virtuel Windows.
2. Télécharger hello ZIP dans votre compte de stockage Azure comme un objet blob. Pour cela, à l’aide d’un outil disponible en externe pour le téléchargement des objets BLOB tooAzure stockage. Il est recommandé de toouse un objet blob privé. Prenez note de l’URL de blob hello du contenu ZIP hello.
3. Activez hello case **déployer un JDK à partir d’un téléchargement personnalisé**.
    Si vous souhaitez toodownload à partir de votre compte de stockage Azure, sélectionnez le compte de stockage hello dans hello **compte de stockage** liste déroulante (vous pouvez cliquer sur hello **comptes** lien toomodify Nouveautés dans la liste de hello), action renseigne partiellement Bonjour **URL** champ, puis renseignez hello portion restante de l’URL de hello. Si vous ne souhaitez pas toouse le stockage Azure, sélectionnez **(aucun)** de hello **compte de stockage** déroulante liste, puis entrez les tooyour d’URL hello JDK télécharger Bonjour **URL** champ. Si vous utilisez le stockage Azure, les noms d’objet blob dans hello URL doivent être en minuscules.
4. Vérifiez que hello **JAVA_HOME** textbox désigne le nom de répertoire correct toohello. Par défaut, elle fait référence hello du même nom de répertoire JDK en tant que valeur hello choisie pour votre usage local. Mais si le répertoire hello contenue dans hello ZIP porte un nom différent (par exemple, échéance toousing une version différente), nom de répertoire de mise à jour hello Bonjour **JAVA_HOME** zone de texte en conséquence, étant donné que ce paramètre est utilisé dans hello cloud () pas dans l’émulateur de calcul hello).
5. Cliquez sur **OK** toosave vos modifications.

Vous avez terminé. Désormais, lorsque vous générez pour le cloud de hello, vous remarquerez taille du package hello sera beaucoup plus petite, les processus de génération hello doivent prend généralement moins de temps et déploiement hello lui-même lorsque vous publiez toohello cloud doit également prendre moins de temps. Notez que hello **déployer mon JDK local (stockage toocloud de chargement automatique)** ou **déployer un JDK à partir d’un téléchargement personnalisé** options sont uniquement en vigueur lorsque votre application est déployée dans le cloud de hello. Ils n’ont aucun effet sur votre expérience d’émulateur de calcul ; version locale de Hello des composants de hello sera toujours être utilisée lorsque vous déployez l’émulateur de calcul toohello. 

### <a name="server-configuration"></a>Configurer le serveur
Hello Voici un exemple de comment vous pouvez spécifier un serveur d’applications.

![][ic796926]

Vérifiez que hello **déployer un serveur de ce type** case à cocher est sélectionnée, puis choisissez le type de hello du serveur d’applications, vous souhaitez toouse.

Pour spécifier un toouse de serveur pour le déploiement de cloud computing, vous pouvez tirer parti de hello options suivantes :

1. **Déployer un serveur de tiers 3e disponible sur Azure** -cela s’applique en particulier dans les scénarios de développement/test où l’efficacité du déploiement et la simplicité est une priorité et serveur de hello ne nécessite pas une configuration personnalisée. Ou toouse un de ces serveurs en tant que point de départ de hello, mais vous incluez les étapes de personnalisation du serveur approprié dans la logique de démarrage de votre déploiement.
2. **Déployer à partir d’un téléchargement personnalisé** -il s’agit applique en particulier dans les scénarios de production lorsque vous avez un serveur spécialement préparé et configuré, que vous souhaitez toouse dans le cloud de hello.
3. **Déployer l’installation de mon serveur local** : cette option s’applique plus particulièrement si l’installation de votre serveur local est déjà configurée et personnalisée pour vous. Si vous choisissez cette option, vous devez également spécifier le chemin d’accès de votre serveur local Bonjour **le chemin d’accès au serveur Local** zone de texte ci-dessous.

Si vous utilisez hello **déployer un serveur de tiers 3e disponible sur Azure** option :

1. Activez hello case **déployer un serveur de tiers 3e disponible sur Azure**.
2. À partir du menu déroulant de hello, sélectionnez toouse de logiciel serveur hello souhaitée avec votre déploiement dans le cloud de hello. Notez que si vous déjà spécifié un type de toouse server précédemment, vous serez limité toochoosing un seul serveur cloud qui se trouve dans hello même famille que ce type de serveur. Mais si vous n’avez pas choisi un type de serveur, vous pouvez choisir de n’importe quel serveur hello qui sont actuellement disponibles sur Azure et le type de serveur hello sera automatiquement sélectionné pour vous.
3. Cliquez sur **OK** toosave vos modifications.

Si vous utilisez hello **déployer à partir d’un téléchargement personnalisé** option :

1. Assurez-vous que vous avez sélectionné un type de serveur en fonction de toohello étapes précédentes. Cela indique à plug-in hello comment serveur hello de toodeploy à partir de votre téléchargement personnalisé, tel qu’il doit être de hello même famille que votre type de serveur sélectionné.
2. Activez hello case **déployer à partir d’un téléchargement personnalisé**.
    Si vous souhaitez toodownload à partir de votre compte de stockage Azure, sélectionnez le compte de stockage hello dans hello **compte de stockage** liste déroulante (vous pouvez cliquer sur hello **comptes** lien toomodify Nouveautés dans la liste de hello), action renseigne partiellement Bonjour **URL** champ, puis renseignez hello portion restante de hello URL tooyour serveur téléchargement le fichier ZIP (lors de l’utilisation du stockage Azure, les noms d’objet blob dans l’URL de hello doit être en minuscule). Si vous ne souhaitez pas toouse le stockage Azure, sélectionnez **(aucun)** de hello **compte de stockage** déroulante liste, puis entrez de téléchargement de serveur hello URL tooyour ZIP Bonjour **URL** champ. contiendrait un dossier enfant représentant votre répertoire d’installation de server application Hello ZIP. Par exemple, si vous utilisez un fichier zip pour Apache Tomcat 7.0.35, au sein de hello zip serait hello enfant dossier représentant hello répertoire d’installation, tel que **tomcat-apache-7.0.35**. 
3. Spécifiez la valeur hello pour la variable d’environnement hello répertoire de base. Il prend par défaut valeur toohello utilisée pour votre serveur d’applications local, si une, mais vous pouvez spécifier une autre valeur si votre serveur d’applications cloud est différente de votre serveur d’applications local. Toutefois, vous devez toomake assurer que votre serveur d’applications cloud est Hello même famille comme type de serveur hello sélectionné précédemment.
    Si vous mettez à jour votre zip de serveur d’application cloud Bonjour futures, vous pouvez modifier manuellement les paramètre du répertoire de base hello ou toohave qu’il corresponde à nouveau à votre paramètre local (si vous avez modifié votre serveur d’applications local trop).
4. Cliquez sur **OK** toosave vos modifications.

Hello sous-jacent logique pour lequel les éléments s’affichent dans hello **Server** onglet Hello **Configuration du serveur** page de propriétés peut être personnalisée. Il s’agit d’une fonctionnalité avancée que vous devrez peut-être si vos besoins dépassent les valeurs par défaut de hello ou si vous souhaitez tooadd autres serveurs. logique de hello toocustomize, Bonjour **Server** boîte de dialogue, cliquez sur hello **personnaliser** lien. Cela entraînera la fermeture hello **Configuration du serveur** page de propriétés et ouvrez hello **componentsets.xml** fichier dans Eclipse, que vous pouvez modifier en tant que modèle de configuration de serveur nécessaires tooextend hello. Documentation de **componentsets.xml** est inclus dans hello **componentsets.xml** fichier lui-même.

Si vous utilisez hello **déployer mon serveur local (stockage toocloud de chargement automatique)** option :

1. Activez hello case **déployer mon serveur local (stockage toocloud de chargement automatique)**.
2. À l’aide de hello **compte de stockage** la liste déroulante, sélectionnez **(auto)**. Si vous spécifiez **(auto)** ici, hello Eclipse toolkit utilisera hello compte de stockage pour votre serveur hello celui que vous sélectionnez pour votre déploiement Bonjour **publier tooAzure** boîte de dialogue.
3. Cliquez sur **OK** toosave vos modifications.

Sélectionnez un chemin d’installation de serveur sur votre ordinateur Bonjour **le chemin d’accès au serveur Local** zone de texte si une de hello conditions suivantes est vraie :

* Vous souhaitez tootest votre déploiement dans l’émulateur hello (s’applique tooWindows uniquement).
* Vous souhaitez toodeploy votre cloud de toohello serveur installé localement.
* Vous souhaitez que toouse un téléchargement de serveur personnalisé de votre propre dans cloud hello, auquel cas, vérifiez également hello **déployer mon serveur local (stockage toocloud de chargement automatique)** option est sélectionnée ci-dessus.

Si aucun des hello précédant options s’appliquent tooyour situation, le paramètre du serveur local hello est facultative.

### <a name="applications-configuration"></a>Configuration des applications
Hello Voici un exemple de comment vous pouvez spécifier une application.

![][ic719512]

Cliquez sur **ajouter** tooadd une autre application, ou **supprimer** tooremove une application. Par souci d’efficacité, si vous voulez toouse un téléchargement pour la source de hello d’une application lors du déploiement de cloud de toohello, utilisez hello [propriétés des composants](#components_properties) toospecify une URL, le compte de stockage, etc.. 

À partir de hello version d’avril 2014, vos applications sont automatiquement téléchargées dans hello même compte de stockage (sous hello **eclipsedeploy** conteneur) que celle sélectionnée pour votre déploiement hello. logique de démarrage Hello de votre déploiement contient une étape qui télécharge tout d’abord ces applications à partir de ce compte de stockage. Cela signifie que vous pouvez mettre à niveau vos applications dans votre déploiement sans avoir besoin de toorebuild et redéployer l’ensemble du package hello, en téléchargeant manuellement les versions plus récentes de l’application hello directement dans ce compte de stockage (en utilisant par exemple hello portail Azure) , en remplaçant les fichiers WAR hello de télécharger à l’origine par les outils d’analyse hello. Ensuite, procédez hello recyclage de toutes ces instances de rôle à l’aide du portail de gestion de Azure, ou via les utilitaires de ligne de commande. (Déclencher le recyclage de rôle directement à partir de la boîte à outils Eclipse hello est actuellement pas en charge.)

### <a name="notes-about-server-configuration"></a>Notes au sujet de la configuration du serveur
Les modifications apportées via hello **configuration du serveur** page de propriétés sont répercutées dans hello `<component>` éléments du fichier package.xml de hello.

Lorsque vous utilisez hello **charger automatiquement...**  ou **déployer depuis un téléchargement...**  options pour hello JDK ou le serveur d’applications et vous générez pour le cloud hello (pas émulateur de calcul hello) et que vous êtes connecté toohello réseau, vous remarquerez peut-être générer des messages tels que suivants de hello dans la sortie de Console hello, comme hello Ant Générateur vérifie la disponibilité du téléchargement hello :

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Si vous avez sélectionné hello **déployer depuis un téléchargement...**  option, hello suivant l’avertissement peut s’afficher, mais hello génération continue :

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Cet avertissement est hello seule indication que hello disponibilité du téléchargement n’a pas été vérifiée. Par conséquent, si un déploiement échoue dans le cloud de hello pour une raison quelconque, vous devez vérifier toosee si vous avez reçu cet avertissement.

Si vous souhaitez la vérification du téléchargement toodisable hello (par exemple, si vous pensez que cela ralentit inutilement de build de hello), affectez la valeur hello `verifydownloads` trop d’attributs`false` Bonjour `<windowsazurepackage>` élément du fichier package.xml : 

`<windowsazurepackage verifydownloads="false" ...>` 

Si vous avez sélectionné hello **charger automatiquement...**  option, puis dans la fenêtre de console hello, vous verrez build messages signaler la progression du téléchargement de hello toutes les 5 secondes, chaque fois qu’un téléchargement est nécessaire hello.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>Propriétés de déchargement SSL
Ouvrez le menu contextuel hello rôle de hello dans le volet Explorateur de projets d’Eclipse, cliquez sur **Azure**, puis cliquez sur **déchargement SSL**. 

![][ic719481]

Cette boîte de dialogue, vous pouvez activer SSL déchargement, ce qui permet des activer tooeasily protocole sécurisé HTTPS (Hypertext Transfer) prend en charge dans votre déploiement Java sur Azure, sans que vous ayez tooconfigure SSL dans votre serveur d’applications Java. Pour plus d’informations, consultez [déchargement SSL] [ SSL Offloading] et [comment tooUse déchargement SSL][How tooUse SSL Offloading].

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse]

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Propriétés du projet Azure][Azure Project Properties]

[Liste des comptes de stockage Azure][Azure Storage Account List]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
