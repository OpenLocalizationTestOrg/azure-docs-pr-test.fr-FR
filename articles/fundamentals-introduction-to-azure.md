---
title: aaaIntro tooMicrosoft Azure | Documents Microsoft
description: "Nouvelle tooMicrosoft Azure ? Obtenir une vue d’ensemble de hello services qu’il propose des exemples de la façon dont ils sont utiles."
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Présentation de Microsoft Azure
Microsoft Azure est la plateforme d’application de Microsoft pour le cloud public de hello.  Hello cet article vise toogive vous une base pour comprendre les notions de base hello d’Azure, même si vous ne connaissez pas quoi que ce soit sur le cloud computing.

**Comment tooread cet article**

Azure augmente tout temps hello afin qu’il soit facile tooget surchargé.  Démarrer avec les services de base hello, qui sont répertoriés en premier dans cet article, puis passez tooadditional services. Qui ne signifie pas que vous ne pouvez pas utiliser uniquement des services supplémentaires hello par eux-mêmes, mais les services de base hello composent core hello d’une application en cours d’exécution dans Azure.

**Envoyer des commentaires**

Vos commentaires sont très importants pour nous. Cet article a été rédigé pour vous offrir un aperçu complet d'Azure. Si elle n’est pas le cas, nous dire dans la section des commentaires hello bas hello de page de hello. Donner des détails sur ce que vous attendiez toosee et comment tooimprove hello article.  

## <a name="hello-components-of-azure"></a>Hello composants de Azure
Azure regroupe des services dans des catégories dans le portail de gestion de hello et des aides visuelles différentes comme hello [What ' s graphisme d’information Azure](https://azure.microsoft.com/documentation/infographics/azure/) . Portail de gestion de Hello est ce que vous utilisez toomanage plus (mais pas la totalité) des services dans Azure.

Cet article utilise un **autre organisation** tootalk sur les services basés sur toocall services secondaire important qui font partie des plus grands et de fonction similaires.  

![Composants Azure](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *Figure : Azure fournit des services d’application accessibles via Internet, exécutés depuis les centres de données Azure.*

## <a name="management-portal"></a>Portail de gestion
Azure a une interface web appelée hello [portail de gestion](http://manage.windowsazure.com) qui permet aux administrateurs tooaccess et administrer les fonctionnalités de la plupart des, mais pas tous Azure.  En général, Microsoft publie portail hello d’interface utilisateur plus récente dans la version bêta avant de retirer un ancien. Hello une version plus récente est appelée hello [« Portail Azure Preview »](https://portal.azure.com/).

Lorsque les deux portails sont activés, leurs fonctionnalités se chevauchent en grande partie. Les services de base sont présents dans les deux portails. Il est cependant possible que les fonctionnalités ne soient pas toutes disponibles dans les deux portails. Services plus récentes peuvent apparaît dans hello plus récente portail premier et antérieures services et fonctionnalités ne peuvent exister que dans hello ancien.  message de type Hello ici est que si vous ne trouvez pas quelque chose dans l’ancien portail de hello, vérifier une version plus récente de hello et vice versa.

## <a name="compute"></a>Calcul
Une des opérations de base hello qu'est d’une plateforme de cloud est d’exécuter des applications. Chacun des modèles de calcul Azure hello possède son propre tooplay de rôle.

Vous pouvez utiliser ces technologies séparément ou les combiner selon les besoins toocreate hello droite foundation pour votre application. approche Hello vous choisissez varie sur les problèmes que vous essayez de toosolve.

### <a name="azure-virtual-machines"></a>Machines virtuelles Azure
![Machines virtuelles Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*Figure : Machines virtuelles vous donne un contrôle total sur les instances de machine virtuelle dans le cloud de hello.*

possibilité de Hello toocreate un ordinateur virtuel à la demande, si à partir d’une image standard ou d’un site que vous fournissez, peut être très utile. Cette approche, communément appelée « Infrastructure as a Service » (IaaS) est celle adoptée par les machines virtuelles Azure. La figure 2 montre une combinaison d’une Machine virtuelle (VM) s’exécute et découvrez comment toocreate un à partir d’un disque dur virtuel.  

toocreate une machine virtuelle, vous spécifiez le disque dur virtuel toouse et hello de taille de machine virtuelle.  Vous payez puis pendant hello que hello que machine virtuelle est en cours d’exécution. Vous payez par minute de hello et uniquement pendant son exécution, s’il existe un coût de stockage minimale de conservation hello disponible de disque dur virtuel. Azure offre une galerie de disques durs virtuels (appelés « images ») qui contiennent un toostart de système d’exploitation amorçable à partir de stock. Ceux-ci comprennent des options Microsoft ainsi que des options partenaires, comme Windows Server et Linux, SQL Server, Oracle et bien d'autres. Vous êtes libre toocreate disques durs virtuels et les images et les téléchargez vous-même. Vous pouvez même télécharger des disques durs virtuels contenant uniquement des données, puis y accéder depuis vos machines virtuelles en cours d'exécution.

Partout où provient de hello disque dur virtuel, vous pouvez stocker de manière persistante toutes les modifications apportées pendant l’exécution d’une machine virtuelle. Hello lorsque vous créez une machine virtuelle à partir de ce disque dur virtuel, choses récupéreront où vous l’avez laissé. Hello disques durs virtuels hello dans des Machines virtuelles sont stockés dans des objets BLOB Azure Storage, ce qui nous aborderons plus tard.  Cela signifie que vous obtenez tooensure redondance que vos machines virtuelles ne sont pas disparaître en raison de défaillances de disque et de toohardware. Il également possible toocopy hello modifié de disque dur virtuel en dehors d’Azure, puis l’exécuter localement.

Votre application s’exécute dans un ou plusieurs ordinateurs virtuels, en fonction de comment vous avez créé avant ou que vous décidez toocreate il à partir de rien maintenant.

Toocloud de cette approche générale très informatique peut être utilisé tooaddress nombreux problèmes.

**Scénarios relatifs à Azure Virtual Machines**

1. **Développement/Test** -vous pouvez utiliser les toocreate une plateforme de développement et de test peu coûteuse qui peut être arrêté lorsque vous avez terminé. Vous pouvez également choisir de créer et d’exécuter des applications utilisant le langage et la bibliothèque que vous préférez. Ces applications peuvent utiliser une des options de gestion des données hello fournis par Azure, et vous pouvez également choisir toouse SQL Server ou un autre SGBD en cours d’exécution dans un ou plusieurs ordinateurs virtuels.
2. **Déplacer des Applications tooAzure (courbes d’élévation et MAJ)** -« Courbes d’élévation et MAJ » fait référence toomoving votre application beaucoup comme vous utiliseriez un toomove chariot un objet volumineux.  Vous « finesse » hello du disque dur virtuel à partir de votre centre de données local et « déplace » tooAzure et exécutez.  Vous aurez généralement toodo certaines dépendances tooremove de travail sur d’autres systèmes. Si ces dépendances sont trop nombreuses, vous pouvez opter pour l'option 3.  
3. **Extension de votre centre de données** - Une autre possibilité est d'utiliser les machines virtuelles Azure comme extension de votre centre de données local pour exécuter SharePoint ou d'autres applications. toosupport, il est possible toocreate des domaines Windows dans le cloud de hello en exécutant Active Directory dans des machines virtuelles Azure. Vous pouvez utiliser le réseau virtuel Azure (mentionné plus loin) tootie votre réseau local et votre réseau dans Azure ensemble.

### <a name="web-apps"></a>Web Apps
![Azure Web Apps ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *Figure : Les applications Web Azure s’exécute une application de site Web dans hello cloud sans avoir de serveur web sous-jacent de toomanage hello.*

Un des hello principales choses dans le cloud de hello est exécuté sites et applications web. Machines virtuelles permet cela, mais il subsiste responsabilité hello d’administration d’un ou plusieurs ordinateurs virtuels et hello sous-jacent des systèmes d’exploitation. Les rôles web Cloud Services peuvent s'en charger, mais leur déploiement et leur gestion nécessitent malgré tout des tâches d'administration.  Que se passe-t-il si vous souhaitez simplement un site Web où quelqu'un d’autre prend en charge de travail d’administration de hello pour vous ?

C’est exactement ce que fournit Web Apps. Ce modèle de calcul offre un environnement web géré à l’aide du portail de gestion Azure hello, ainsi que des API. Vous pouvez déplacer une application de site Web existant dans les applications Web inchangée, ou vous pouvez créer une nouvelle directement dans le cloud de hello. Une fois qu’un site Web est en cours d’exécution, vous pouvez ajouter ou supprimer des instances dynamiquement, partie de confiance sur équilibrer les demandes Azure Web Apps tooload entre eux. Applications Azure offre une option partagée, où votre site Web s’exécute dans un ordinateur virtuel avec d’autres sites, et une option standard qui permet à un site toorun dans sa propre machine virtuelle. Hello standard vous permet également augmenter la taille hello (puissance de calcul) de vos instances si nécessaire.

Pour le développement, Web Apps prend en charge .NET, PHP, Node.js, Java et Python, de même que la base de données SQL et MySQL (de ClearDB, un partenaire Microsoft) pour le stockage relationnel. La prise en charge de plusieurs applications populaires, notamment WordPress, Joomla et Drupal est également intégrée. Hello vise tooprovide un faible coût, évolutif et une plateforme largement utile pour la création de sites et applications web dans un cloud public hello.

**Scénarios Web Apps**

Web Apps est utile pour les entreprises, les développeurs et les organismes de conception web de toobe prévue. Les entreprises bénéficient d'une solution simple à gérer, évolutive, hautement sécurisée et très disponible pour leurs sites web. Lorsque vous devez tooset un site Web, il est meilleure toostart avec Azure Web Apps et continuer tooCloud Services une fois que vous avez besoin d’une fonctionnalité qui n’est pas disponible. Voir en fin de hello de section de « Calcul » hello pour des liens supplémentaires qui peuvent aider à vous toochoose entre les options hello.

### <a name="cloud-services"></a>Services cloud
![Service cloud Azure](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*Figure : Azure Cloud Services fournit un code personnalisé place toorun hautement évolutive sur une plateforme comme un environnement de Service (PaaS)*

Supposons que vous souhaitiez toobuild une application de cloud qui prend en charge un grand nombre d’utilisateurs simultanés, ne requiert pas occuper de l’administration et jamais tombe en panne. Vous pouvez être un fournisseur de logiciels établi, par exemple, c’est la décision tooembrace logiciel en tant que Service (SaaS) par la génération d’une version de l’un de vos applications dans le cloud de hello. ou que vous soyez une start-up créatrice d’une application au potentiel prometteur, si vous travaillez dans Azure, quel modèle d’exécution devez-vous choisir ?

Azure Web Apps vous permet de créer ce type d’applications web, mais avec certaines contraintes. Par exemple, vous ne bénéficiez pas d’accès administrateur, ce qui signifie que vous ne pouvez pas installer de logiciel arbitrairement. Machines virtuelles Azure vous offre une grande souplesse, y compris l’accès d’administration et certainement utilisez-le toobuild une application très évolutive, mais vous disposerez toohandle nombreux aspects de la fiabilité et l’administration. Vous aimeriez est une option qui vous donne hello contrôle que vous avez besoin, mais gère également la plupart du travail hello requis pour l’administration et de fiabilité.

C’est exactement ce que proposent les services cloud Azure. Cette technologie est conçue expressément toosupport évolutif et fiable et les applications de faible-admin, et il est un exemple de ce qu’on appelle généralement plateforme en tant que Service (PaaS). toouse, vous créez une application à l’aide de la technologie hello vous choisissez, tel que c#, Java, PHP, Python, Node.js ou quelque chose d’autre. Ensuite, votre code s’exécute sur des machines virtuelles (instances tooas visés) exécutant une version de Windows Server.

Mais ces machines virtuelles sont distincts des hello celles que vous créez avec des Machines virtuelles Azure. Il faut savoir qu’Azure les gère lui-même (par exemple, pour l’installation de correctifs du système d’exploitation, le déploiement automatique de nouvelles images avec correctifs, etc. Cela implique que votre application ne doit pas maintenir l’état dans les instances de rôle web ou de travail ; Il doit être conservée dans une des options de gestion de données Azure hello décrites dans la section suivante de hello. Azure surveille également ces machines virtuelles et les redémarre en cas d'échec. Vous pouvez définir des cloud services tooautomatically créer des instances plus ou moins dans toodemand de réponse. Ainsi, vous toohandle augmente l’utilisation et puis mise à l’échelle pour que vous ne sont pas payer autant moins d’utilisation.

Vous avez deux rôles toochoose, lorsque vous créez une instance, toutes deux basées sur Windows Server. Hello principale différence hello deux est qu’une instance d’un rôle web exécute IIS n’est pas le cas d’une instance d’un rôle de travail. Les deux sont gérés Bonjour même façon, toutefois et courant pour un toouse d’application à la fois. Par exemple, une instance de rôle web peut accepter les demandes des utilisateurs, puis les transmettre l’instance de rôle de travail tooa pour le traitement. tooscale votre application vers le haut ou vers le bas, vous pouvez demander que Azure créer plusieurs instances de chaque rôle ou arrêter les instances existantes. Et similaires tooAzure de Machines virtuelles, vous êtes facturé uniquement pour les temps de hello que chaque instance de rôle web ou de travail est en cours d’exécution.

**Scénarios relatifs à Azure Cloud Services**

Services de cloud computing sont toosupport idéale massive avec montée en puissance quand un contrôle renforcé sur la plateforme de hello que fournis par les applications Web Azure, mais n’avez pas besoin de contrôle du système d’exploitation sous-jacent hello.

#### <a name="choosing-a-compute-model"></a>Choix d'un modèle de calcul
page de Hello [comparaison Azure Web Apps, Services de cloud computing et Machines virtuelles](app-service-web/choose-web-site-cloud-service-vm.md) fournit plus d’informations sur la façon de toochoose un modèle de calcul.

## <a name="data-management"></a>Gestion des données
Les applications ont besoin de données, et chaque type d’application a besoin de données différentes. Pour cette raison, Azure fournit plusieurs façons différentes toostore et gérer les données. Azure propose de nombreuses options de stockage, toutes conçues pour un stockage de très longue durée.  Avec une de ces options, il existe toujours 3 copies de vos données restent synchronisées dans un centre de données Azure--6 si vous autorisez tooback de géo-redondance toouse Azure des centres de données tooanother au moins 300 miles.     

### <a name="in-virtual-machines"></a>Machines virtuelles
possibilité de Hello toorun SQL Server ou un autre SGBD dans une machine virtuelle créée avec des Machines virtuelles Azure a déjà été mentionné. Notez que cette option n’est pas limité toorelational systèmes ; vous êtes également libre toorun des technologies de NoSQL comme MongoDB et Cassandra. Votre propre système de base de données en cours d’exécution est simple informatique réplique notre utilisé tooin nos propres centres de données- mais elle nécessite également la gestion des administration hello de ce système SGBD.  D’autres options, Azure gère plusieurs ou l’ensemble de l’administration hello pour vous.

Là encore, état hello Hello Machine virtuelle et n’importe quel disque de données supplémentaires, vous créez ou que vous téléchargez sont accompagnés de stockage d’objets blob (dont nous parlons plus loin).  

### <a name="azure-sql-database"></a>Base de données SQL Azure
![Azure Storage - SQL Database](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*Figure : Base de données SQL Azure fournit un service de base de données relationnelle managés dans le cloud de hello.*

Pour le stockage relationnel, Azure fournit la fonctionnalité de hello de base de données SQL. Trompeur hello d’affectation de noms. Elle n’a rien à voir avec la base de données SQL fournie par SQL Server et exécutée sur l’infrastructure Windows Server.  

Anciennement SQL Azure, base de données SQL Azure fournit toutes les hello principales fonctionnalités d’une base de données relationnelle système de gestion, y compris les transactions atomiques, accès concurrentiel aux données par plusieurs utilisateurs avec l’intégrité des données, les requêtes SQL ANSI et une programmation familier modèle. Tout comme SQL Server, SQL Database est accessible via Entity Framework, ADO.NET, JDBC et les autres principales technologies d’accès aux données. Il prend également en charge la plupart des hello langage T-SQL, ainsi que des outils SQL Server tels que SQL Server Management Studio. Pour toute personne familière avec SQL Server (ou toute autre base de données relationnelle), l’utilisation de la base de données SQL ne devrait poser aucun problème.

Mais la base de données SQL n’est pas simplement un SGBD Bonjour informatique cloud d’un service PaaS. Tout de même contrôler de vos données et qui est accessible, mais la base de données SQL prend en charge de travail d’administration grunt hello, telles que la gestion d’infrastructure de matériel hello et conservation automatiquement des logiciels de base de données et le système d’exploitation hello des toodate. SQL Database offre également une haute disponibilité, des sauvegardes automatiques, des fonctionnalités de récupération jusqu'à une date et une heure, et peut répliquer des copies d'une zone géographique vers une autre.  

**Scénarios relatifs à SQL Database**

Si vous créez une application Windows Azure (à l’aide d’un des modèles de calcul hello) qui a besoin de stockage relationnel, base de données SQL peut être une bonne option. Applications cloud de hello extérieur en cours d’exécution permet également ce service, cependant, il y a beaucoup d’autres scénarios. Par exemple, les données stockées dans SQL Database sont accessibles à partir de différents systèmes client, dont les ordinateurs de bureau, les ordinateurs portables, les tablettes et les téléphones. L’utilisation de SQL Database permet de réduire les temps d’arrêt grâce à la réplication qui assure une haute disponibilité intégrée.

### <a name="tables"></a>Tables
![Azure Storage - Tables](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*Figure : Tables Azure fournit une plat NoSQL de toostore données.*

Cette fonctionnalité porte parfois d'autres noms, car elle fait partie d'une fonctionnalité plus large appelée « Azure Storage ». Si vous voyez « tables », « tables Azure » ou « tables de stockage », il est tout hello même chose.  

Et ne vous inquiétez pas par nom de hello : stockage relationnel ne fournit pas cette technologie. Il s'agit en fait d'un exemple d'approche NoSQL appelé « stockage clé/valeur ». Les tables Azure permettent à une application de stocker différents types de propriétés, comme des chaînes, des nombres entiers et des dates. Une application peut ensuite récupérer un groupe de propriétés en fournissant une clé unique pour ce groupe. Alors que les opérations complexes telles que les jointures ne sont pas prises en charge, les tables envoient des données de tootyped d’un accès rapide. Ils sont également très évolutives, avec un toohold en mesure de table unique jusqu'à un téraoctet de données. Et correspondant à leur simplicité, les tables sont généralement moins coûteuse toouse que le stockage relationnel de la base de données SQL.

**Scénarios relatifs aux tables Azure**

Supposons que vous vouliez toocreate une application Azure qui a besoin d’accélérée accéder aux données de tootyped, cette opération peut prendre beaucoup de, mais n’a pas besoin de tooperform des requêtes SQL complexes sur ces données. Par exemple, imaginez que vous créez une application consommateur qui a besoin d’informations de profil de client toostore pour chaque utilisateur. Votre application va toobe très populaire, donc vous devez tooallow pour un grand nombre de données, mais vous ne suffit pas avec ces données au-delà de stockage, puis l’extraction dans des moyens simples. C’est exactement hello type de scénario dans lequel les Tables Azure de sens.

### <a name="blobs"></a>Objets blob
![Azure Storage Blobs](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*Figure : les objets blob Azure fournissent des données binaires non structurées.*  

Objets BLOB Windows Azure (nouveau « Stockage d’objets Blob » et simplement « objets BLOB de stockage » sont hello même chose) est conçue toostore des données binaires non structurées. Tout comme les tables, les objets blob offrent un stockage économique, et la taille d'un objet blob peut atteindre 1 To (un téraoctet). Les applications Azure peuvent également utiliser les lecteurs Azure, qui permettent aux objets blob de proposer un stockage permanent pour un système de fichiers Windows monté sur une instance Azure. application Hello voit les fichiers Windows ordinaires, mais hello contenu est réellement stocké dans un objet blob.

Le stockage d'objets blob est utilisé par beaucoup d'autres fonctionnalités Azure (y compris par Virtual Machines), ce qui permet également de gérer vos charges de travail.

**Scénarios relatifs aux objets blob**

Une application stockant des vidéos, des fichiers volumineux ou d'autres informations binaires peut utiliser les objets blob pour assurer un stockage simple et peu onéreux. Souvent, les objets blob sont aussi utilisés en association avec d'autres services, comme le réseau de distribution de contenu (CDN) sur lequel nous nous pencherons ultérieurement.  

### <a name="import--export"></a>Import/Export
![Azure Import Export Service](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*Figure : Windows Azure, importez / Export fournit hello capacité tooship un tooor de disque dur physique à partir de Azure pour l’importation de données en bloc plus rapide et économique ou d’exportation.*  

Parfois, vous voulez toomove une grande quantité de données dans Azure. Cette opération peut prendre beaucoup de temps, plusieurs jours parfois, et utiliser beaucoup de bande passante. Dans ce cas, vous pouvez utiliser Azure Import/Export, ce qui permet de vous tooship chiffré par Bitlocker 3,5" disques durs SATA directement tooAzure des centres de données, où Microsoft transférera les données de salutation dans le stockage d’objets blob pour vous.  Après la fin du téléchargement hello, Microsoft est fourni tooyou arrière de lecteurs hello.  Vous pouvez également demander que grandes quantités de données à partir du stockage d’objets Blob à exporter sur des disques durs et à envoyer tooyou différé par courrier.

**Scénarios relatifs à Azure Import/Export**

* **Migration de données volumineux** - dès que vous avez de grandes quantités de données (téraoctets) que vous souhaitez tooupload tooAzure, hello service Import/Export est souvent beaucoup plus rapide et peut-être moins chère que transférer sur hello internet. Une fois les données de salutation dans des objets BLOB, vous pouvez le traiter dans d’autres formats tels que le stockage de Table ou une base de données SQL.
* **Archivé la récupération des données** -vous pouvez utiliser Import/Export toohave Microsoft transfèrent de grandes quantités de données stockées dans le stockage d’objets Blob Azure tooa dispositif de stockage que vous envoyez, puis ce périphérique remis emplacement tooa arrière de votre choix. Dans la mesure où ce transfert prend du temps, cette solution ne convient pas à la récupération d'urgence. Elle convient davantage aux données archivées auxquelles vous n'avez pas besoin d'accéder rapidement.

### <a name="file-service"></a>Service de fichiers
![Azure File Services](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*Figure : Fournit des Services de fichiers Azure SMB \\ \\server\share les chemins d’accès pour les applications en cours d’exécution dans le cloud de hello.*

En local, il est commun toohave de grandes quantités de stockage de fichiers accessible via hello de protocole Server Message Block (SMB) à l’aide un \\ \\Server\share format. Azure a maintenant un service qui vous permet de toouse ce protocole dans le cloud de hello. Les applications s’exécutant dans Azure peuvent utiliser tooshare des fichiers entre les machines virtuelles à l’aide des API comme ReadFile et WriteFile système de fichiers familier. En outre, les fichiers hello peuvent également y accéder à hello simultanément via une interface REST, qui vous permet de partages de hello tooaccess localement lorsque vous configurez également un réseau virtuel. Fichiers Azure s’appuie sur le service d’objets blob hello, afin qu’il hérite hello même disponibilité, la durabilité, l’évolutivité et géo-redondance de stockage Azure.

**Scénarios relatifs à Azure Files Services**

* **Migration cloud existant du toohello applications** -son plus facile toohello cloud toomigrate localement les applications qui utilisent le fichier de partage des données de tooshare entre les parties de l’application hello. Chaque machine virtuelle connecte partage de fichiers toohello et puis peut lire et écrire des fichiers exactement comme elle serait par rapport à un fichier local partager.
* **Application de paramètres partagés** -il est courant pour les applications distribuées toohave des fichiers de configuration dans un emplacement centralisé où ils sont accessibles à partir de nombreux ordinateurs virtuels différents. Ces fichiers de configuration peuvent être stockés dans un partage Azure Files, puis lus par toutes les instances de l'application. Hello paramètres peuvent également être gérés via l’interface REST hello, qui autorise l’accès dans le monde toohello les fichiers de configuration.
* **Partage de diagnostic** - Vous pouvez enregistrer et partager des fichiers de diagnostic comme des journaux, des indicateurs de performances et des vidages sur incident. Ces fichiers disponibles à travers l’interface REST et hello SMB autorise applications toouse des outils d’analyse pour traiter et analyser les données de diagnostic hello.
* **Développement/Test/Debug** : quand les développeurs ou administrateurs fonctionnent sur des machines virtuelles dans le cloud de hello, ils doivent souvent un ensemble d’outils ou utilitaires. L'installation et la distribution de ces utilitaires sur chaque machine virtuelle prennent du temps. Avec des fichiers Azure, un développeur ou un administrateur peut stocker leurs outils favoris sur un partage de fichiers et se connecter toothem à partir de n’importe quel ordinateur virtuel.

## <a name="networking"></a>Mise en réseau
Azure s’exécute dès aujourd'hui dans plusieurs centres de données répartis Bonjour. Lorsque vous exécutez une application ou stockez des données, vous pouvez sélectionner un ou plusieurs de ces toouse de centres de données. Vous pouvez également connecter toothese des centres de données de différentes manières, à l’aide des services de hello ci-dessous.

### <a name="virtual-network"></a>Réseau virtuel
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*Figure : Réseaux virtuels fournit un réseau privé dans le cloud de hello pour différents services peuvent communiquer avec tooeach autres ou ressources locales tooon si vous configurez un réseau VPN intersite.*  

Un moyen utile toouse un cloud public est tootreat comme une extension de votre centre de données.

Comme vous pouvez créer des machines virtuelles à la demande, puis les supprimer (et ainsi arrêter la facturation) lorsque vous n’en avez plus besoin, vous disposez de toute la puissance informatique, juste quand vous en avez besoin. Et, étant donné que les Machines virtuelles Azure vous permet de créer des machines virtuelles exécutant SharePoint et autres logiciels familière locale Active Directory, cette approche peut fonctionner avec les applications hello que vous avez déjà.

toomake ce vraiment utile, cependant, vos utilisateurs doivent tootreat en mesure de toobe ces applications comme si elles étaient exécutées dans votre centre de données. C’est exactement ce que propose le réseau virtuel Azure. À l’aide d’un périphérique de passerelle VPN, un administrateur peut configurer un réseau privé virtuel (VPN) entre votre réseau local et vos ordinateurs virtuels qui sont déployés tooa réseau virtuel dans Azure. Étant donné que vous attribuez vos propres cloud de toohello des adresses IP v4 machines virtuelles, elles apparaissent toobe sur votre réseau. Les utilisateurs de votre organisation peuvent accéder à des applications de hello de ces machines virtuelles contiennent comme si elles étaient exécutées localement.

Pour plus d'informations sur la planification et la création d'un réseau virtuel, consultez la rubrique [Virtual Network](virtual-network/virtual-networks-overview.md).

### <a name="express-route"></a>ExpressRoute
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*Figure : Utilise ExpressRoute un réseau virtuel Azure, mais les connexions via des itinéraires plus rapidement dédié lignes au lieu de hello Internet public.*  

Si vous avez besoin de bande passante supplémentaire ou si vous souhaitez bénéficier d'une sécurité supérieure à celle que peut fournir une connexion Azure Virtual Network, vous pouvez opter pour ExpressRoute. Dans certains cas, ExpressRoute peut également vous faire économiser de l'argent. Vous devez toujours un réseau virtuel dans Azure, mais le lien hello entre Azure et votre site utilise une connexion dédiée ne passe pas par hello Internet public. Dans commande toouse ce service, vous devez toohave un accord avec un fournisseur de services réseau ou un fournisseur exchange.

Configurer une connexion ExpressRoute nécessite plus de temps et de planification, vous pouvez donc toostart avec un VPN de site à site, puis migrer tooan connexion ExpressRoute.

Pour plus d'informations sur ExpressRoute, consultez la rubrique [ExpressRoute - Aperçu technique](expressroute/expressroute-introduction.md).

### <a name="traffic-manager"></a>Traffic Manager
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*Figure : Azure Traffic Manager permet de vous tooroute globales du trafic tooyour service en fonction des règles intelligents.*

Si votre application Windows Azure est en cours d’exécution dans plusieurs centres de données, vous pouvez utiliser Azure Traffic Manager tooroute demandes d’utilisateurs intelligemment entre les instances de l’application hello. Vous pouvez également acheminer le trafic tooservices ne pas en cours d’exécution dans Azure tant qu’ils sont accessibles à partir de hello internet.  

Une application Windows Azure avec des utilisateurs dans une seule partie Bonjour peut s’exécuter dans un seul centre de données Azure. Une application avec des utilisateurs éparpillés Bonjour, toutefois, est plus probable toorun dans plusieurs centres de données, peut-être même tous les. Dans ce deuxième cas, vous êtes confronté à un problème : comment intelligemment et déployer les instances de tooapplication les utilisateurs ? La plupart du temps de hello, vous souhaiterez probablement chaque tooher utilisateur tooaccess hello centre de données le plus proche, étant donné que vous donnera probablement son temps de réponse meilleures hello. Mais que se passe-t-il si cette instance de l’application hello est surchargé ou non disponible ? Dans ce cas, c’est le cas être, nice toodirect sa demande automatiquement tooanother le centre de données. C’est exactement le rôle d’Azure Traffic Manager.

propriétaire Hello d’une application définit les règles qui spécifient comment les demandes des utilisateurs doivent être dirigée toodatacenters, puis s’appuie sur toocarry Traffic Manager ces règles. Par exemple, les utilisateurs pourraient normalement être dirigée toohello de centre de données Azure le plus proche, mais envoyées tooanother un lorsque le temps de réponse hello dans leur centre de données par défaut dépasse le temps de réponse hello à partir d’autres centres de données. Pour les applications distribuées globalement comportant de nombreux utilisateurs, un problème toohandle service intégré est utile.

Traffic manager utilise des points de terminaison Service de nom de répertoire (DNS) tooroute utilisateurs tooservice, mais plus le trafic ne passe pas par le biais de Traffic Manager une fois que cette connexion est établie. Traffic Manager ne se transforme ainsi pas en goulot d'étranglement susceptible de ralentir vos communications de service.

## <a name="developer-services"></a>Services de développement
Azure offre un nombre d’outils toohelp développeurs et professionnels de l’informatique, créer et gérer des applications dans le cloud de hello.  

### <a name="azure-sdk"></a>Kit de développement logiciel (SDK) Azure
En 2008, hello première version préliminaire de Azure pris en charge uniquement le développement .NET. Aujourd’hui, vous pouvez créer des applications Azure dans la quasi-totalité des langages. Actuellement, Microsoft fournit des Kits de développement logiciel (SDK) spécifiques pour .NET, Java, PHP, Node.js, Ruby et Python. Il existe aussi un Kit de développement logiciel (SDK) Azure général qui assure une prise en charge de base pour tous les langages, tels que C++.  

Ces Kits de développement logiciel (SDK) vous aident à créer, à déployer et à gérer vos applications Azure. Ils sont disponibles sur [www.microsoftazure.com](https://azure.microsoft.com/downloads/) ou GitHub et peuvent être utilisés avec Visual Studio et Eclipse. Azure propose également des outils de ligne de commande qui permet aux développeurs avec n’importe quel environnement éditeur ou de développement, y compris les outils de déploiement tooAzure d’applications à partir des systèmes Linux et Macintosh.

En plus de vous aider à concevoir des applications Azure, ces Kits de développement logiciel (SDK) fournissent des bibliothèques clientes qui vous permettent de créer des logiciels utilisant les services Azure. Par exemple, vous pourrez générer une application qui lit et écrit des objets BLOB Windows Azure, ou créer un outil qui déploie des applications Azure via l’interface de gestion Azure hello.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services est un nom de marketing couvrant un nombre des services qui permettent aux applications toodevelop Bonjour Azure.

tooavoid confusion - il ne fournit pas une version hébergée ou basée sur le Web de Visual Studio. Une copie locale en cours d'exécution de Visual Studio est requise. Mais vous avez accès à des outils supplémentaires qui peuvent se révéler très utiles.

Le système de contrôle de code source hébergé Team Foundation Service est également fourni pour le contrôle de version et le suivi des éléments de travail.  Pour le contrôle de version, vous pouvez également utiliser Git. Et vous pouvez varier le système de contrôle de source de hello que vous utilisez par projet. Vous pouvez créer des projets d’équipe privé illimitées accessible à partir de n’importe où dans Bonjour.  

Visual Studio Team Services fournit un service de test de charge. Vous pouvez exécuter des tests de charge créés dans Visual Studio sur des machines virtuelles dans le cloud de hello. Vous spécifiez le nombre total de hello d’utilisateurs test tooload avec, et Visual Studio Team Services automatiquement déterminer le nombre d’agents est nécessaires, lancer des machines virtuelles de hello requis et exécuter vos tests de charge. Si vous êtes abonné à MSDN, vous bénéficiez chaque mois de milliers de minutes gratuites pour les tests de charge.

Visual Studio Team Services prend également en charge le développement agile avec des fonctionnalités comme les builds d’intégration continue, les tableaux Kanban et les salles d’équipe virtuelles.

**Scénarios Visual Studio Team Services**

Visual Studio Team Services est une bonne option pour les entreprises qui doivent toocollaborate dans le monde entier et n’avez pas encore infrastructure de hello dans place toodo donc. Vous pouvez procéder à la configuration en quelques minutes, choisir un système de contrôle du code source et commencer à créer le code et la build le jour même.  outils d’équipe Hello fournissent un emplacement pour la coordination et la collaboration et des outils supplémentaires hello fournissent l’analyse de hello nécessaire tootest et paramétrer votre application rapidement.

Mais les entreprises qui possèdent déjà un système local peuvent tester des projets dans Visual Studio Team Services toosee s’il est plus efficace.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*Figure : Application Insights surveille les performances et l’utilisation de votre site web en ligne ou de votre application.*

Quand vous avez publié votre application, qu’elle s’exécute sur des appareils mobiles, des ordinateurs de bureau ou des navigateurs web, Application Insights vous indique comment elle fonctionne et ce que les utilisateurs font avec elle. Il conserve un nombre d’incidents et de réponse lent, alerte si les chiffres hello dépasser les seuils inacceptables et vous aider à diagnostiquer les problèmes.

Lorsque vous développez une nouvelle fonctionnalité, vous pouvez planifier toomeasure son succès avec les utilisateurs. En analysant les modèles d’utilisation, vous comprenez ce qui convient le mieux à vos clients et vous améliorez votre application lors de chaque cycle de développement.

Bien qu’il soit hébergé dans Azure, Application Insights fonctionne pour une large gamme d’applications, à la fois sur Azure et en dehors. Les applications web J2EE et ASP.NET sont couvertes, ainsi que les applications iOS, Android, OSX et Windows. Télémétrie est envoyé à partir d’un kit de développement logiciel généré avec l’application hello, toobe analysées et affichées dans hello service Application Insights dans Azure.

Si vous souhaitez plus spécialisée analytique, exportation hello télémétrie flux tooa base de données ou tooPower BI ou d’autres outils.

**Scénarios Application Insights**

Vous développez une application. Il peut s’agir d’une application web ou d’une application pour appareil, ou d’une application d’appareil avec un serveur web principal.

* Régler les performances de hello de votre application après sa publication, ou bien qu’il soit de test de charge.  Application Insights agrège la télémétrie de toutes les instances de hello installé et vous propose des graphiques de temps de réponse de demande et nombre d’exceptions, les temps de réponse de dépendance et autres indicateurs de performance. Ceux-ci vous aident à optimiser les performances de votre application. Vous pouvez insérer le code tooreport si vous avez besoin des données plus spécifiques.
* Détectez et diagnostiquez les problèmes dans votre application en direct. Vous pouvez recevoir des alertes par e-mail si les indicateurs de performances dépassent les seuils acceptables. Vous pouvez examiner les sessions utilisateur spécifique, par exemple les demande hello toosee a causé une exception.
* Effectuer le suivi de la réussite de hello tooassess d’utilisation de chacune des nouvelles fonctionnalités. Lorsque vous créez un nouveau récit utilisateur, planifiez toomeasure combien il est utilisé, et si les utilisateurs leurs objectifs attendus. Application Insights vous donne les données d’utilisation de base tels que les vues de page web, et vous pouvez insérer le code tootrack hello l’expérience utilisateur plus en détail.

### <a name="automation"></a>Automatisation
Personne n’aime temps toowaste hello manuel même traite plusieurs fois. Azure Automation fournit un moyen pour toocreate, surveiller, gérer et déployer des ressources dans votre environnement Azure.  

Automation utilise « runbooks », qui utilise des flux de travail Windows PowerShell (par opposition à PowerShell habituels) dans les coulisses de hello. Procédures opérationnelles sont censées toobe exécutée sans intervention de l’utilisateur. Flux de travail PowerShell permet hello l’état d’un toobe script enregistré à des points de contrôle hello moyen. Si une défaillance se produit, il est inutile toostart un script à partir du début de hello. Vous pouvez le redémarrer au dernier point de contrôle hello. Cela vous permet d’économiser beaucoup de travail de la tentative de handle de script hello toomake tous les échecs possibles.

**Scénarios relatifs à Azure Automation**

Azure Automation est un manuel de hello tooautomate bon choix, les longs, erreurs et les tâches répétitives dans Azure.

### <a name="api-management"></a>API Management
Création et la publication des Interfaces de programmation d’Application (API) sur hello internet est une tooapplications de services tooprovide moyen commun. Si ces services sont revendable (par exemple, les données météorologiques), une organisation peut autoriser des tiers tooaccess aux mêmes services gratuitement. Lorsque vous faites évoluer toomore partenaires, vous aurez généralement besoin toooptimize et contrôler l’accès.  Certains partenaires peuvent même être amené à données hello dans un format différent.

Gestion des API Azure facilite pour les organisations toopublish API toopartners, employés et des développeurs tiers en toute sécurité et à grande échelle. Il fournit un point de terminaison API différentes et agit comme un proxy toocall hello point de terminaison réel tout en offrant des services tels que la mise en cache, la transformation, la limitation, contrôle d’accès et agrégation de l’analytique.

**Scénarios relatifs au service Gestion des API**

Supposons que votre entreprise possède un ensemble d’appareils qu’il faut alors toocall tooa arrière service central tooget données--par exemple, une société de transport qui dispose d’appareils dans chaque camion sur route de hello.  Société de hello est préférable de tooset d’un tootrack système, il est propres camions afin de prédire et mettre à jour des délais de diffusion de façon fiable. Elle pourra connaître le nombre de camions dont elle dispose et effectuer des prévisions appropriées.  Chaque camion devez un appareil qui rappelle tooa point central avec son positionnement et la vitesse des données et qui est peut-être plus.

Un client de la société d’expédition de hello aurait probablement également bénéficier de l’obtention de ces données de positionnement.  client de Hello pourrait utiliser tooknow amplitude produits ont tootravel, où ils coincés, combien ils payer le long de certaines liaisons (s’il est combiné avec qu’ils payant tooship). Si la société d’expédition de hello regroupe ces données déjà, de nombreux clients peuvent payer.  Mais hello société d’expédition doit ensuite tooprovide un moyen toogive clients hello des données. Une fois qu’elles fournissent l’accès toocustomers, ils peuvent rencontrer pas contrôler la fréquence à laquelle hello interrogation des données. Ils les règles tooprovide concernant qui peuvent accéder aux données. Toutes ces règles aurait toobe intégrée à son API externe. C'est là que Gestion des API Azure peut s'avérer utile.  

## <a name="identity-and-access"></a>Identité et accès
La plupart des applications fonctionnent avec des identités. En connaissant l'identité d'un utilisateur, l'application sait comment elle doit interagir avec lui. Azure fournit l’identité de suivi toohelp services ainsi que les intégrer à des magasins d’identités vous utilise peut-être déjà.

### <a name="active-directory"></a>Active Directory
Comme la plupart des services d’annuaire Azure Active Directory stocke des informations sur les utilisateurs et des organisations hello qu'auquel ils appartiennent. Il permet aux utilisateurs de se connecter, puis les fournit avec les jetons qu’ils peuvent présenter tooapplications tooprove leur identité. Il permet de synchroniser les informations utilisateur avec Windows Server Active Directory exécuté sur votre réseau local. Alors que les mécanismes de hello et formats de données utilisés par Azure Active Directory ne sont pas identiques à ceux utilisés dans Windows Server Active Directory, les fonctions hello qu’il exécute sont assez semblables.

Son important toounderstand que Azure Active Directory est conçue essentiellement pour une utilisation par les applications cloud. Il peut être utilisé par les applications exécutées sur Azure ou sur d’autres plateformes de cloud. Il est également utilisé par les applications en nuage de Microsoft, telles que celles dans Office 365. Si vous souhaitez tooextend de votre centre de données en nuage hello à l’aide de Machines virtuelles Azure et réseau virtuel Azure, toutefois, Azure Active Directory n’est pas idéale hello. Au lieu de cela, vous souhaiterez toorun Windows Server Active Directory dans des Machines virtuelles.

les applications toolet accéder aux informations hello qu’il contient, Azure Active Directory fournit une API RESTful appelé Azure Active Directory Graph. Cette API permet aux applications en cours d’exécution sur toute plateforme accès et Active les relations hello entre eux.  Par exemple, une application d’autorisés peut utiliser cette toolearn API sur un utilisateur, il appartient à des groupes de hello et d’autres informations. Applications peuvent également voir les relations entre les utilisateurs en leur sociale graphique-vous permettant de les utiliser plus intelligemment des connexions hello entre des personnes.

Une autre fonctionnalité de ce service, Azure Active Directory Access Control, plus facilement une application tooaccept identité des informations à partir de Facebook, Google, Windows Live ID et autres fournisseurs d’identité. Au lieu d’obliger hello application toounderstand hello divers formats de données et les protocoles utilisés par chacun de ces fournisseurs, le contrôle d’accès tous les traduit en un format commun unique. Il permet aussi à l’application d’accepter des identifiants provenant d’un ou de plusieurs domaines Active Directory. Par exemple, un fournisseur qui fournit une application SaaS peut-être utiliser les utilisateurs de contrôle d’accès Azure Active Directory toogive dans chacun de son application toohello de l’authentification unique de clients.

Les services d’annuaire sont une composante essentielle de l’informatique en local. Il ne doit pas être surprenant qu’ils sont également importantes dans le cloud de hello.

### <a name="multi-factor-authentication"></a>Azure Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*Figure : Multi-Factor Authentication fournit des fonctionnalités hello pour tooverify de votre application à plusieurs formes d’identification*

La sécurité est un élément toujours important. L'authentification multi-facteur (MFA - Multi-factor authentication) permet de veiller à ce que seuls les utilisateurs aient accès à leurs comptes. Pour l'authentification multi-facteur (ou authentification à deux facteurs), les utilisateurs doivent fournir deux de ces trois méthodes de vérification de l'identité pour les connexions et transactions des utilisateurs.

* Un élément que vous connaissez (généralement un mot de passe)
* Un élément que vous possédez (un appareil de confiance qui n'est pas facilement dupliqué, comme un téléphone)
* Un élément vous concernant particulièrement (biométrie)

Donc lorsqu’un utilisateur se connecte, vous pouvez exiger qu’ils tooalso vérifient leur identité avec une application mobile, d’un appel téléphonique ou d’un message texte en association avec son mot de passe. Par défaut, Azure Active Directory prend en charge hello des mots de passe comme unique méthode d’authentification pour les connexions utilisateur. Vous pouvez utiliser l’authentification Multifacteur avec Azure AD ou avec des applications personnalisées et de répertoires à l’aide de hello MFA SDK. Vous pouvez également l'utiliser avec des applications locales à l'aide du serveur Azure Multi-Factor Authentication.

**Scénarios relatifs à MFA**

Protection des identifiants de connexion aux comptes sensibles comme les comptes bancaires et l'accès au code source pour lesquels un accès non autorisé peut avoir un coût important sur le plan financier ou sur le plan de la propriété intellectuelle.   

## <a name="mobile"></a>Mobile
Si vous créez une application pour un appareil mobile, Azure peut aider à stocker des données dans le cloud de hello, d’authentifier les utilisateurs et d’envoyer des notifications push sans que vous ayez toowrite une grande quantité de code personnalisé.

Pendant que vous pouvez certainement créer principal hello pour une application mobile à l’aide d’ordinateurs virtuels, des Services de cloud computing ou des applications Web, vous pouvez perdre beaucoup moins hello de l’écriture de temps sous-jacent de composants de service à l’aide des services de Azure.

### <a name="mobile-apps"></a>Mobile Apps
![Mobile Apps](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*Figure : Mobile Apps fournit la fonctionnalité généralement requise par les applications qui font office d’interface avec les appareils mobiles.*

Azure Mobile Apps contient de nombreuses fonctionnalités utiles qui peuvent vous faire gagner un temps précieux lors de la conception de l’infrastructure d’une application mobile. Il vous permet de toodo simplicité de la configuration et la gestion des données stockées dans une base de données SQL. Avec un code côté serveur, vous pouvez facilement utiliser des options de stockage supplémentaires, telles que le stockage d'objets blob ou MongoDB. Mobile Apps prend les notifications en charge. Cela dit, dans certains cas, vous pouvez utiliser Notification Hubs, comme décrit plus loin.  service de Hello possède également une API REST que votre application mobile peut appeler tooget le travail effectué. Applications mobiles permet également hello tooauthenticate des utilisateurs via Active Directory et Microsoft, ainsi que les autres fournisseurs d’identité bien connus tels que Facebook, Twitter et Google.   

Vous pouvez utiliser d’autres Services Azure tels que le Service Bus et les rôles de travail et vous connecter à des systèmes de site tooon. Vous pouvez même utiliser 3e partie modules complémentaires hello fonctionnalités supplémentaires de tooprovide Azure Store (comme SendGrid pour le courrier électronique).

Bibliothèques clientes native pour Android, iOS, HTML/JavaScript, Windows Phone et Windows Store rendent toodevelop plus facile pour les applications sur toutes les principales plateformes mobiles. Une API REST permet toouse données Mobile Services et fonctionnalités d’authentification avec les applications sur différentes plateformes. Un service mobile unique peut être utilisé pour plusieurs applications clientes. Vous pouvez ainsi offrir une expérience utilisateur cohérente sur différents appareils.

Azure prend en charge la mise à l’échelle massive déjà, vous pouvez gérer le trafic de hello à mesure que votre application plus populaire.  Analyse et la journalisation sont pris en charge toohelp résoudre les problèmes et gérer les performances.

### <a name="notification-hubs"></a>Notification Hubs
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*Figure : Notification Hubs fournit la fonctionnalité généralement requise par les applications qui font office d’interface avec les appareils mobiles.*

Pendant que vous pouvez écrire du code toodo notifications dans les applications mobiles Azure, concentrateurs de Notification est optimisé toobroadcast des millions de notifications push personnalisées dans les minutes.  Vous n’avez pas tooworry sur les détails, tels que l’opérateur mobile ou le fabricant du périphérique. Vous pouvez cibler des utilisateurs individuels ou des millions d'utilisateurs avec un seul appel d'API.

Concentrateurs de notification est conçue toowork avec n’importe quel serveur principal. Vous pouvez utiliser les applications mobiles Azure, un principal personnalisé dans le cloud hello en cours d’exécution sur n’importe quel fournisseur ou un serveur principal local.

**Scénarios de concentrateur de notification** si vous écrivez un jeu mobile où les lecteurs a eu active, vous devrez peut-être toonotify lecteur 2 joueur 1 terminée à son tour. S’il vous suffit toodo, vous pouvez utiliser uniquement des applications mobiles. Mais si vous aviez 100 000 utilisateurs lire votre jeu et que vous souhaitez toosend fois tooeveryone sensibles offre gratuite, concentrateurs de Notification est hello meilleur choix.

Vous pouvez envoyer des informations de dernière minute, sportives produit annonce notifications toomillions d’utilisateurs et les événements avec une faible latence. Les entreprises peuvent avertir leurs employés sur les nouvelles communications sensibles temps, telles que les prospects, pour que les employés n’aient tooconstantly vérifier les messages électroniques ou autres toostay applications informé. Vous pouvez également envoyer les mots de passe à usage unique requis pour l'authentification multi-facteur.

## <a name="back-up"></a>Sauvegarde
Chaque entreprise doit toobackup et restaurer des données. Vous pouvez utiliser Azure toobackup et restaurer votre application cloud de hello ou local. Azure offre toohelp différentes options en fonction de type hello de sauvegarde.

### <a name="site-recovery"></a>Site Recovery
Azure Site Recovery (anciennement Hyper-V Recovery Manager) peut vous aider à protéger les applications importantes en coordonnant la réplication de hello et la récupération entre les sites. Récupération de site fournit des applications de tooprotect fonctionnalité basé sur Hyper-v, VMWare ou SAN tooyour propre site secondaire, site l’hébergeur tooa ou tooAzure et éviter les coûts de hello et la complexité de la création et la gestion de votre propre emplacement secondaire. Azure chiffre les données et les communications et vous pouvez hello activer le chiffrement de données au repos trop.

Il surveille l’intégrité de hello de vos services en continu et vous aide à automatiser la récupération de façon ordonnée hello de services dans l’événement hello d’une panne de site au centre de données principal hello. Machines virtuelles peut être mis dans un service de restauration de manière orchestré toohelp rapidement, même pour les charges de travail complexes à plusieurs niveaux.

Azure Site Recovery utilise des technologies existantes telles que Réplica Hyper-V, System Center et SQL Server Always On. Pour plus de détails, consultez la [vue d’ensemble Azure Site Recovery](site-recovery/site-recovery-overview.md) .

### <a name="azure-backup"></a>Azure Backup
![Sauvegarde Azure](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*Figure : Azure sauvegarde des données à partir de serveurs de Windows local dans le cloud de hello.*  

Sauvegarde Azure sauvegarde les données à partir de serveurs locaux exécutant Windows Server dans le cloud de hello. Vous pouvez gérer vos sauvegardes directement à partir des outils de sauvegarde hello dans Windows Server 2012, Windows Server 2012 Essentials ou System Center 2012 - Data Protection Manager. Vous pouvez également utiliser un agent de sauvegarde spécialisé.

Les données sont mieux sécurisées, car les sauvegardes sont chiffrées avant la transmission, stockées et chiffrées dans Azure et protégées par un certificat que vous téléchargez. service de Hello utilise hello même niveau de protection des données redondantes et hautement disponible trouvé dans le stockage Azure.  Vous pouvez sauvegarder les fichiers et dossiers à intervalles réguliers ou immédiatement, et exécuter des sauvegardes complètes ou incrémentielles. Une fois les données sauvegardées toohello cloud, les utilisateurs autorisés peuvent facilement récupérer serveur tooany de sauvegardes. Il offre également des stratégies de rétention de données configurable, la compression de données et transfert de données de limitation afin de gérer des données toostore et le transfert du coût hello.

**Scénarios relatifs à Azure Backup**

Si vous utilisez déjà Windows Server ou System Center, Azure Backup est une solution idéale pour sauvegarder le système de fichiers de votre serveur, vos machines virtuelles et vos bases de données SQL Server.  Il fonctionne avec des fichiers chiffrés, partiellement alloués et compressés. Il existe certaines limitations, donc vous devez [vérifier les conditions préalables Azure Backup hello](http://technet.microsoft.com/library/dn296608.aspx) première.

## <a name="messaging-and-integration"></a>Messagerie et intégration
Quel que soit son activité, le code doit fréquemment toointeract avec un autre code.  Dans certaines situations, une simple messagerie de base en file d’attente suffit. Dans d’autres, des interactions plus complexes sont nécessaires. Azure fournit plusieurs façons différentes toosolve ces problèmes. La figure 5 illustre les choix de hello.

### <a name="queues"></a>Files d’attente
![Azure Service Bus Relay](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*Figure : les files d’attente permettent d’associer des éléments d’une application et facilitent la mise à l’échelle.*  

La mise en file d’attente est une idée simple : une application place un message dans une file d’attente afin qu’il soit ensuite lu par une autre application. Si votre application doit simplement ce service simple, les files d’attente Azure peut être hello meilleur choix.

En raison de hello de façon hello Qu'azure a augmenté au fil du temps, les files d’attente de stockage Azure et files d’attente de Service Bus fournissent des services de file d’attente similaires. raisons Hello pourquoi vous souhaiteriez toouse une sur hello autres sont traités dans le livre de techniques hello [Azure files d’attente et Service Bus - comparaison et différences](http://msdn.microsoft.com/library/azure/hh767287.aspx).  Dans de nombreux scénarios, celles-ci peuvent être utilisées indifféremment.

**Scénarios relatifs aux files d’attente**

Une utilisation courante des files d’attente est aujourd'hui toolet une instance de rôle web communiquer avec une instance de rôle de travail au sein de hello même application de Services de cloud computing.

Par exemple, supposons que vous créez une application de partage vidéo avec Azure. application Hello se compose du code PHP en cours d’exécution dans un rôle web qui permet aux utilisateurs téléchargent et regarder des vidéos, ainsi que d’un rôle de travail implémentée en c# qui traduit téléchargé vidéo dans différents formats.

Lorsqu’une instance de rôle web obtienne une nouvelle vidéo à partir d’un utilisateur, il peut stocker des vidéo de hello dans un objet blob, puis envoyer un rôle de travail de message tooa via une file d’attente lui indiquant où toofind cette nouvelle vidéo. Une instance de rôle de travail-it n’importe quel message hello-un sera puis lecture de file d’attente hello et effectue hello requis des traductions vidéo en arrière-plan de hello.

Structuration d’une application de cette façon permet le traitement asynchrone, et rend hello tooscale plus facile d’application, étant donné que le nombre de hello d’instances de rôle web et des instances de rôle de travail peut être modifiée indépendamment. Vous pouvez également utiliser la taille de file d’attente hello en tant que déclencheur tooscale hello nombre de rôles de travail haut et bas. Lorsque cette taille augmente, vous pouvez ajouter de nouveaux rôles. Lorsqu’il atteint inférieur, vous pouvez réduire le nombre hello de l’exécution de rôles toosave money.  

Vous pouvez utiliser ce même modèle entre de nombreux éléments différents de votre application, même s'ils n'utilisent pas de rôles de travail/web.  Il vous permet de parties de hello tooscale de chaque côté de la file d’attente de hello haut et bas en tant que la demande et nécessite du temps de traitement.

### <a name="service-bus"></a>Service Bus
Si elles s’exécutent dans le cloud hello, dans votre centre de données sur un appareil mobile ou un autre endroit, les applications doivent toointeract. Bonjour Azure Service Bus vise toolet les applications en cours d’exécution pratiquement n’importe quel endroit échangent des données.

Dans Ajout toohello files d’attente (un-à-un) décrits plus haut, Service Bus fournit également tooother méthodes de communication.

#### <a name="service-bus-relay"></a>Service Bus Relay
![Azure Service Bus Relay](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*Figure : Service Bus Relay permet la communication entre des applications situées de chaque côté d’un pare-feu.*

Service Bus permet une communication directe via son service de relais, fournissant une toointeract de manière sécurisée à travers des pare-feu. Relais Service Bus activer des applications toocommunicate en échangeant des messages via un point de terminaison hébergé dans le cloud de hello, plutôt que localement.

**Scénarios relatifs à Service Bus Relay**

Les applications qui communiquent via Service Bus peuvent être des applications Azure ou des logiciels exécutés sur une autre plateforme cloud. Ils peuvent également être des applications qui s’exécutent en dehors du cloud de hello, toutefois. On peut prendre l’exemple d’une compagnie aérienne qui implémente ses services de réservation sur des ordinateurs au sein de son propre centre de données. billet d’avion Hello doit tooexpose ces clients de réduire de services, y compris les bornes archiver dans un aéroport, terminaux de l’agent de réservation et les téléphones encore clients. Il peut utiliser Service Bus toodo cela, création de diverses applications faiblement couplées d’interactions entre hello.

#### <a name="service-bus-topics-and-subscriptions"></a>Rubriques et abonnements Service Bus
![Rubriques d’Azure Service Bus](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *Figure : Rubriques Service Bus permet à plusieurs applications toopost messages et autres applications toosubscribe tooreceive qui répondent aux critères spécifiques.*

Service Bus contient un mécanisme de publication et d'abonnement appelé Rubriques et abonnements. Avec Oriented, une application peut envoyer rubrique tooa de messages, tandis que les autres applications peuvent créer la rubrique toothis d’abonnements. Cela permet la communication un-à-plusieurs entre un ensemble d’applications, vous permettant de hello même message d’être lu par plusieurs destinataires.

**Scénarios pour les rubriques et abonnements Service Bus**

Chaque fois que vous configurez dans lequel il existe de nombreux messages sont importants, mais différents systèmes en aval n’ont besoin des sous-ensembles de toodiffering toolisten de ces communications, rubrique Service Bus et les abonnements sont un bon choix.

### <a name="biztalk-services"></a>BizTalk Services
![BizTalk Services](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *Figure : Fournit des Services BizTalk formats de messages hello capacité tootransform XML dans le cloud de hello.*

Il est parfois nécessaire de relier des systèmes qui communiquent à l'aide de différents formats de messagerie. Il est courant pour les schémas de base de données différente toohave commercial et XML messagerie formats, même lorsqu’une norme commune est disponible. Plutôt que d’écrire une grande quantité de code personnalisé, vous pouvez utiliser BizTalk Server sur site toointegrate différents systèmes.  Fournit des Services BizTalk Azure hello même type de service, mais dans le cloud de hello. Vous pouvez payer uniquement ce que vous utilisez et vous inquiétez pas sur l’échelle comme il vous faudrait tooon local.

**Scénarios relatifs à BizTalk Services**

Les interactions interentreprises requièrent généralement ce type de traduction.  Par exemple, une entreprise de génération avions besoins des parties de tooorder à partir de celui-ci est différents fournisseurs de composants. Il aura plusieurs fournisseurs de pièces.  Ces commandes doivent être automatisé toogo directement à partir de systèmes de générateurs d’avion hello dans les systèmes de fournisseurs hello.  Aucune entreprise veut toochange leurs systèmes de base et les formats de message, et il est peu probable que ces formats sont hello identiques. Les Services BizTalk peut accepter des messages et les convertir entre les deux méthodes nouveaux formats de hello. Un fournisseur d’avion hello faire hello travail tootranslate ou hello différents fournisseurs peut, en fonction de qui veut quantité plus de contrôle et hello de traduction si nécessaire.     

## <a name="compute-assistance"></a>Assistance au calcul
Azure fournit une assistance pour les services qui ne doivent pas toorun tout temps hello.  

### <a name="scheduler"></a>Scheduler
![Azure Scheduler](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*Figure : Azure Scheduler fournit un moyen tooschedule travaux à un moment donné pour une durée spécifique.*

Parfois, les applications doivent uniquement toorun à un moment donné. Sur Azure, vous pouvez enregistrer money avec ce type d’application au lieu de laisser une application simplement conserver en cours d’exécution en attente de données tooprocess 24 x 7. Azure Scheduler vous permet de tooschedule lorsqu’une application doit s’exécuter en fonction de l’intervalle de temps ou d’un calendrier. Ce service particulièrement fiable vérifie qu'un processus est en cours d'exécution, même en cas de défaillance du réseau, de l'ordinateur et du centre de données. Vous utilisez hello API REST de Scheduler toomanage ces actions.

Lorsqu’une alarme planifiée se produit, le planificateur envoie HTTP ou HTTPS messages tooa point de terminaison spécifique ou peut placer un message dans une file d’attente de stockage.  Par conséquent, vous devez toohave votre application ont un point de terminaison accessible ou qu’il surveiller une file d’attente de stockage. Puis une fois qu’il obtient le message de type hello, il peut effectuer n’importe quelle action, il est programmé pour.

**Scénarios relatifs à Scheduler**

* Actions d’application récurrentes : par exemple, un service peut régulièrement obtenir des données de twitter et collecter des données de salutation dans un flux normal.
* Maintenance quotidienne : nettoyage ou traitement des journaux en exécutant des sauvegardes et autres tâches de planification intermittentes.
* Tâches exécutées de nuit.
* Tâches relatives aux applications web, comme les nettoyages quotidiens des journaux en exécutant des sauvegardes et autres tâches de maintenance. Un administrateur peut choisir toobackup sa base de données à 1 h 00 chaque jour pour hello 9 mois à venir, par exemple.

Hello API Scheduler vous permet de toocreate, mettre à jour, supprimer, afficher et gérer des collections de travaux et des travaux planifiés par programmation.

## <a name="performance"></a>Performances
Les performances sont toujours déterminantes pour une application. Les applications ont tendance à tooaccess hello plusieurs fois les mêmes données. Les performances monodirectionnelle tooimprove tookeep une copie de cette application toohello proche de données, les temps de hello réduction nécessaire tooretrieve il. Pour ce faire, Azure propose différents services :

### <a name="azure-caching"></a>Azure Caching
![Azure Caching](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **Figure : une application Azure peut mettre des données en cache dans la mémoire, voire les fractionner entre différents rôles de travail.**

L’accès aux données stockées dans un des services de gestion de données Azure (base de données SQL, tables ou objets blob) est relativement rapide. Mais accéder à des données stockées en mémoire l’est encore plus. C’est pour cela que conserver une copie en mémoire des données fréquemment utilisées peut améliorer les performances des applications. Vous pouvez utiliser cette toodo de mise en cache en mémoire d’Azure.

Une application de Services de cloud computing, vous pouvez stocker des données dans ce cache, puis récupérer directement sans avoir besoin d’un stockage persistant tooaccess. cache de Hello peut être géré à l’intérieur de votre application d’ordinateurs virtuels ou être fournie par les ordinateurs virtuels dédiés toocaching uniquement. Dans les deux cas, cache de hello peut être distribué, avec les données de salutation, il contient réparti entre plusieurs machines virtuelles dans un centre de données Azure.

Azure comporte un certain nombre de technologies de mise en cache qui ont évolué au fil du temps. Dans l’ordre de hello qu’ils ont été introduites, il est partagé, dans le rôle, gérés et le cache Redis. Hello partagé mise en cache est une technologie plus ancienne et que vous ne doivent pas créer de nouvelles implémentations avec lui. Hello Cache géré a hello mêmes fonctionnalités des hello In-Role cache, mais en tant que service géré en dehors de hello portail de gestion Azure. Hello Cache Redis est en version préliminaire. implémentation de Redis Hello a hello plus grand nombre de fonctionnalités et est recommandée lorsque vous écrivez un nouveau code de mise en cache.

**Scénarios relatifs à la mise en cache Azure**

Une application qui lit à plusieurs reprises un catalogue de produits peut bénéficier de l’utilisation de ce type de mise en cache, par exemple, puisque les données hello il a besoin est disponible plus rapidement. la technologie Hello prend également en charge le verrouillage, laisser être utilisé avec la lecture/écriture, ainsi que des données en lecture seule. Et les applications ASP.NET peuvent utiliser les données de session hello service toostore avec seulement une modification de configuration.

### <a name="content-delivery-network"></a>Réseau de distribution de contenu
![Azure CDN](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **Figure : Copies d’un objet blob peuvent être mis en cache dans le monde hello.**

Supposons que vous avez besoin des données blob toostore qui seront accessible aux utilisateurs monde hello. Il est peut-être une vidéo de hello dernière coupe du monde correspondance, par exemple, mises à jour de pilote ou un livre électronique populaires. Vous aide à stocker une copie des données de hello dans plusieurs centres de données Azure, mais s’il existe un grand nombre d’utilisateurs, il n’est probablement pas suffisamment. Pour encore améliorer les performances, vous pouvez utiliser hello Azure CDN.

Hello CDN a des dizaines de sites monde hello, chaque capable de stocker des copies des objets BLOB Windows Azure. Hello première fois un utilisateur dans une partie de hello world accède à un objet blob particulier, les informations de hello qu’il contient sont copiées à partir d’un centre de données Azure dans le stockage local de CDN cette zone géographique. Après cela, l’accès de la partie de hello world utilise copie d’objets blob hello mis en cache dans hello CDN-ils ne doivent toogo toohello de façon hello tous les plus proches du centre de données Azure. résultat de Hello est plus rapide accéder aux données d’elles sonttrop accédé par les utilisateurs n’importe où dans Bonjour.

**Scénarios relatifs à CDN**

Il est commun toouse CDN avec vidéo de toodeliver Media Services dans le monde entier. Les vidéos sont généralement volumineuses et nécessitent beaucoup de bande passante.  Media Services est abordé plus loin sur cette page.

## <a name="big-data-and-big-compute"></a>Big Compute et données volumineuses
### <a name="hdinsight-hadoop"></a>HDInsight (Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **Figure : HDInsight facilite le traitement en bloc de hello de grandes quantités de données**

De nombreuses années, en bloc de hello d’analyse des données a été effectué sur les données relationnelles stockées dans un entrepôt de données généré avec un SGBD. Ce type d’analytique de l’entreprise est important, et il s’agit d’un toocome beaucoup de temps. Mais que se passe-t-il si vous souhaitez tooanalyze les données hello sont tellement volumineuses que les bases de données relationnelles uniquement ne peut pas gérer ? Et supposons que les données de salutation n’est pas relationnelles ? Il peut s’agir, entre autres exemples, de journaux de serveur dans un centre de données ou de données historiques d’événements enregistrés par des capteurs Dans ce cas, données importantes est synonyme de problèmes importants. Il vous faut trouver une autre approche.

la technologie dominante Hello aujourd'hui pour l’analyse des données volumineuses est Hadoop. Un Apache projet open source, cette technologie stocke des données à l’aide de hello système de fichiers distribués Hadoop (HDFS), puis permet aux développeurs de créer tooanalyze des travaux MapReduce ces données. HDFS répartit les données sur plusieurs serveurs, puis les segments s’exécute de tâche MapReduce de hello sur chacun d’eux, laissant les données volumineuses hello être traités en parallèle.

HDInsight est le nom hello de service de Azure hello Apache Hadoop. HDInsight vous permet de HDFS stockent les données sur le cluster de hello et la distribuer sur plusieurs machines virtuelles. Elle propage également la logique d’une tâche MapReduce hello sur ces machines virtuelles. Tout comme avec local Hadoop, données sont logique de traité localement hello et il fonctionne sur les données de salutation sont dans hello même machine virtuelle- et en parallèle pour de meilleures performances. HDInsight peut également stocker des données dans Azure Storage Vault qui utilise des objets blob.  À l’aide de ASV vous permet de toosave money, car vous pouvez supprimer votre cluster HDInsight inutilisés, mais garder vos données dans le cloud de hello.

HDinsight prend en charge les autres composants de l’écosystème de Hadoop hello, y compris Hive et Pig. Microsoft a créé également les composants qui la rendent toowork plus facile avec les données produites par HDInsight à l’aide des Outils BI traditionnels, tels que l’adaptateur HiveODBC hello et Explorateur de données qui fonctionnent avec Excel.

### <a name="high-performance-computing-big-compute"></a>Calculs complexes (Big Compute)
Un des toouse de manières très intéressante hello une plateforme de cloud est toorun informatique de hautes performances (HPC) et d’autres applications « Big Compute ». Exemples spécialisées ingénierie toouse d’applications créées hello normalisées Interface MPI (Message Passing) ainsi que les applications de ces soi-disant, ces modèles de risques financiers.

essentiellement, Big Compute Hello est l’exécution de code sur de nombreuses machines à hello même temps. Sur Azure, cela signifie en cours de plusieurs machines virtuelles simultanément, tout en parallèle toosolve un problème. Cette opération nécessite leur travail à certaines moyen tooresources tooschedule applications et, par exemple, toodistribute entre ces instances. Microsoft gratuit HPC Pack et autres solutions de cluster de calcul peuvent fonctionner correctement dans Azure, en tirant profit de calcul et infrastructure des services Azure tooadd capacité à la demande tooan localement compute cluster ou d’exécutent des applications Big Compute entièrement dans hello cloud.

Azure fournit une plage de machine virtuelle tailles d’instance avec différentes configurations de cœurs du processeur, mémoire, capacité du disque et autres exigences de hello toomeet caractéristiques de différentes applications. Hello récemment introduites A8 et le travail d’instances A9 bien pour de nombreuses calcul charges de travail intensives et des applications MPI parallèles, en particulier, car elles disposent de processeurs multicœurs, grande vitesse et de grandes quantités de mémoire. Dans certains cas de hello configurations tirer parti d’un réseau applicatif à latence faible et haut débit dans le cloud hello qui inclut la technologie direct à la mémoire à distance (RDMA) d’accès pour une efficacité maximale des applications MPI parallèles.

Azure offre également aux développeurs d'applications Big Compute et aux partenaires un ensemble complet de fonctionnalités de calcul, de services, de choix d'architectures et d'outils de développement. Azure prend en charge Big Compute flux de travail personnalisés qui impliquent des workflows de données spécialisée et de projet et la tâche de planification des modèles qui peuvent mettre à l’échelle toothousands de cœurs de calcul.

## <a name="media"></a>Médias
![Azure Media Services](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **Figure : Media Services est une plate-forme pour les applications qui fournissent la vidéo et autres tooclients media monde hello.**

La vidéo prend une part importante du trafic Internet aujourd’hui et cette proportion va continuer à croître. Encore fournissant vidéo sur le web de hello n’est pas simple. Il existe un grand nombre de variables, telles que hello encodage hello et l’algorithme de résolution d’écran de l’utilisateur hello d’affichage. Vidéo tend également toohave les pics de demandes comme un pic samedi soir lorsqu’un grand nombre de personnes choisir toowatch un film en ligne.

En réponse à cette popularité, on peut logiquement penser que de plus en plus de nouvelles applications utiliseront la vidéo. Mais tous les devez toosolve certaines Hello même des problèmes et effectuer chacun d’eux à résoudre ces problèmes sur son propre n’est pas justifiée. Une meilleure approche consiste à toocreate une plateforme qui fournit des solutions courantes pour nombreuses applications toouse. Et création de cette plate-forme dans le cloud de hello a certains avantages. Il peut être largement disponible sur un paiement à l’utilisation, et il peut également gérer la variabilité hello dans la demande qui sont souvent confrontés à des applications vidéos.

Azure Media Services a été développé pour répondre à ces problèmes. Il fournit un ensemble de composants de cloud pour simplifier le travail des personnes chargées de créer et d’exécuter des applications utilisant de la vidéo ou d’autres médias.

Comme le montre la figure hello, Media Services fournit un ensemble de composants pour les applications qui fonctionnent avec vidéo et d’autres supports. Par exemple, il inclut un support vidéo tooupload de composant de réception dans les Services de support (où il est stocké dans des objets BLOB Azure), un composant de codage qui prend en charge différents formats vidéo et audio, un composant de protection du contenu qui fournit la gestion des droits numériques, un composant pour l’insertion de publicités dans un flux vidéo, des composants de diffusion en continu et bien plus encore. Partenaires Microsoft peuvent également fournissent des composants de plateforme de hello, puis demander à Microsoft de distribuer ces composants et de facturation en leur nom.

Les applications qui utilisent cette plateforme peuvent être exécutées sur Azure ou autre. Par exemple, une application de bureau pour un centre de production vidéo peut permettre à ses utilisateurs télécharger tooMedia vidéo Services, puis le traiter de différentes manières. Vous pouvez également un service de gestion de contenu sur le cloud s’exécutant sur Azure peut-être reposent sur Media Services tooprocess et distribuer vidéo. Là où elle s’exécute et tout ce que c’est le cas, chaque application choisit les composants dont il a besoin toouse, en y accédant via des interfaces RESTful.

toodistribute qu’il génère, une application peut utiliser hello Azure CDN, un autre CDN, ou envoyer uniquement les bits directement toousers. Quelle que soit l’origine, les vidéos créées à l’aide de Media Services peuvent être utilisées par divers systèmes clients, notamment Windows, Macintosh, HTML 5, iOS, Android, Windows Phone, Flash et Silverlight. Hello vise toomake il les applications modernes media toocreate plus faciles.

**Informations de référence**

Pour obtenir une vue plus visuelle du fonctionnement de Media Services, téléchargez hello [Azure Media Services Poster][Azure Media Services Poster].

## <a name="commerce"></a>Commerce
lieu de Hello du logiciel en tant que Service consiste à transformer nous comment créer des applications. Les modes de vente des applications évoluent également. Dans la mesure où une application SaaS réside dans le cloud de hello, il est judicieux que ses clients potentiels doivent rechercher des solutions en ligne. Et cette modification s’applique toodata ainsi que tooapplications. Pourquoi ne doivent pas de considérer la toohello cloud pour les datasets disponibles ? Microsoft traite les deux de ces problèmes avec hello [Azure Marketplace](https://azure.microsoft.com/marketplace/).

![Azure Commerce](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **Figure : Azure Marketplace et Azure Store vous permettent de rechercher et d’acheter des applications et ensembles de données commerciales Azure afin de les utiliser avec vos applications Azure.**

Hello différence entre deux de hello est que Marketplace est en dehors de hello portail de gestion Azure, mais hello magasin est accessible à partir d’à l’intérieur du portail de hello. Les clients potentiels peuvent rechercher toofind Azure applications qui répondent à leurs besoins. Les clients peuvent rechercher des ensembles de données commerciales, comme des données démographiques, financières et géographiques. Lorsqu’ils trouver quelque chose qu'ils le souhaitent, ils peuvent y accéder à partir du fournisseur de hello, directement par le biais de hello Marketplace ou des sites web Store ou dans certains cas à partir du portail de gestion de hello. Applications peuvent également utiliser les API de recherche Bing de hello via hello Marketplace, en leur donnant accès toohello des résultats des recherches sur le web.

**Scénarios relatifs à Azure Commerce**

SendGrid est une application hello magasin Azure qui vous permet de toosend messagerie. Cette application offre des fonctionnalités supplémentaires comme une remise fiable et des statistiques.  Vous pouvez acheter cette application et les services associés plutôt que toobuild une telle infrastructure vous-même.  

## <a name="getting-started"></a>Mise en route
Maintenant que vous avez maintenant hello de présentation, hello est toowrite votre première application Azure. Choisissez votre langue, [obtenir hello SDK approprié](/downloads/)et n’hésitez pas. Cloud computing est hello nouvelle valeur par défaut : prise en main.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
