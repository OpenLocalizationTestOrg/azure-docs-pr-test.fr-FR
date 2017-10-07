---
title: "aide-mémoire de performances et l’évolutivité de stockage aaaAzure | Documents Microsoft"
description: "Une liste des pratiques éprouvées à utiliser avec Azure Storage dans le développement d’applications performantes."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2970c055d460070288d1810e4a77a7f056a4137
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage
## <a name="overview"></a>Vue d'ensemble
Depuis la version hello de services de stockage Microsoft Azure hello, Microsoft a développé un nombre de pratiques éprouvées pour l’utilisation de ces services de manière performant, et cet article sert tooconsolidate hello plus importants d'entre eux dans une liste de style de la liste de vérification. intention de Hello de cet article est les développeurs d’applications toohelp vérifier qu’ils utilisent des pratiques éprouvées avec toohelp les identifient les autres pratiques éprouvées, qu'ils doivent envisager l’adoption et le stockage Azure. Cet article ne tente pas de toocover chaque optimisation des performances et évolutivité possible, il exclut les celles qui sont petites dans leur impact ou non largement applicable. étendue toohello hello le comportement de l’application peut être prédite lors de la conception, il est utile tookeep dans à l’esprit dès le début des conceptions tooavoid qui seront exécute dans des problèmes de performances.  

Chaque développeur d’applications à l’aide du stockage Azure doit prendre hello temps tooread cet article et vérifiez que son application suit chaque hello ci-dessous des pratiques éprouvées.  

## <a name="checklist"></a>Liste de contrôle
Cet article organise les pratiques éprouvée de hello en hello les groupes suivants. Pratiques éprouvées applicables aux éléments suivants :  

* Tous les services Azure Storage (objets blob, tables, files d’attente et fichiers)
* Objets blob
* Tables
* Files d’attente  

| Terminé | Domaine | Catégorie | Question |
| --- | --- | --- | --- |
| &nbsp; | Tous les services |Objectifs d'évolutivité |[Votre tooavoid application conçue est proche des objectifs d’évolutivité hello ?](#subheading1) |
| &nbsp; | Tous les services |Objectifs d'évolutivité |[Est votre tooenable conçue de convention d’affectation de noms mieux l’équilibrage de charge ?](#subheading47) |
| &nbsp; | Tous les services |Mise en réseau |[Les périphériques clients côté ont-ils suffisamment large bande passante et les performances de hello tooachieve de faible latence nécessaire ?](#subheading2) |
| &nbsp; | Tous les services |Mise en réseau |[La qualité de la liaison des appareils côté client est-elle suffisamment élevée ?](#subheading3) |
| &nbsp; | Tous les services |Mise en réseau |[Application cliente de hello se trouve « près de « compte de stockage hello ?](#subheading4) |
| &nbsp; | Tous les services |Distribution de contenu |[Utilisez-vous un CDN pour la distribution de contenu ?](#subheading5) |
| &nbsp; | Tous les services |Accès direct au client |[Vous utilisez SAS et CORS toostorage d’un accès direct tooallow au lieu de proxy](#subheading6) |
| &nbsp; | Tous les services |Mise en cache |[Votre application met-elle en cache les données qui sont utilisées fréquemment et qui changent rarement ?](#subheading7) |
| &nbsp; | Tous les services |Mise en cache |[Votre application traite-t-elle les mises à jour par lots (mise en cache côté client, suivie du téléchargement dans des ensembles plus grands) ?](#subheading8) |
| &nbsp; | Tous les services |Configuration .NET |[Vous avez configuré votre toouse client un nombre suffisant de connexions simultanées ?](#subheading9) |
| &nbsp; | Tous les services |Configuration .NET |[Vous avez configuré .NET toouse un nombre suffisant de threads ?](#subheading10) |
| &nbsp; | Tous les services |Configuration .NET |[Utilisez-vous .NET 4.5 ou version ultérieure, qui présente une méthode de nettoyage de mémoire optimisée ?](#subheading11) |
| &nbsp; | Tous les services |Parallélisme |[Vous assurez que parallélisme est limité en conséquence afin que vous ne surchargez pas vos fonctionnalités d’un client ou un objectifs d’évolutivité hello ?](#subheading12) |
| &nbsp; | Tous les services |Outils |[Vous utilisez la version la plus récente de Microsoft hello fourni outils et bibliothèques clientes](#subheading13) |
| &nbsp; | Tous les services |Nouvelle tentatives |[Utilisez-vous une stratégie de nouvelles tentatives d'interruption exponentielle pour les erreurs de limitation et les délais d'expiration ?](#subheading14) |
| &nbsp; | Tous les services |Nouvelle tentatives |[Votre application empêche-t-elle les nouvelles tentatives pour les erreurs non renouvelables ?](#subheading15) |
| &nbsp; | Objets blob |Objectifs d'évolutivité |[Disposez-vous d’un grand nombre de clients qui accèdent simultanément à un seul objet ?](#subheading46) |
| &nbsp; | Objets blob |Objectifs d'évolutivité |[Votre application est rester au sein de la cible de l’évolutivité des opérations ou de la bande passante hello pour un seul objet blob ?](#subheading16) |
| &nbsp; | Objets blob |Copie d'objets blob |[La copie des objets blob s'effectue-t-elle de manière efficace ?](#subheading17) |
| &nbsp; | Objets blob |Copie d'objets blob |[Utilisez-vous AzCopy pour les copies en bloc d'objets blob ?](#subheading18) |
| &nbsp; | Objets blob |Copie d'objets blob |[Vous utilisez Azure Import/Export tootransfer très grands volumes de données ?](#subheading19) |
| &nbsp; | Objets blob |Utilisation de métadonnées |[Stockez-vous des métadonnées fréquemment utilisées concernant des objets blob dans leurs métadonnées ?](#subheading20) |
| &nbsp; | Objets blob |Téléchargement rapide |[Lorsque vous essayez un objet blob de tooupload rapidement, vous téléchargez les blocs en parallèle ?](#subheading21) |
| &nbsp; | Objets blob |Téléchargement rapide |[Lorsque vous essayez tooupload nombreux objets BLOB rapidement, vous téléchargez les objets BLOB en parallèle ?](#subheading22) |
| &nbsp; | Objets blob |Type d'objet blob correct |[Utilisez-vous des objets blob de pages ou de blocs lorsque cela s'avère approprié ?](#subheading23) |
| &nbsp; | Tables |Objectifs d'évolutivité |[Sont vous approchant hello objectifs d’évolutivité pour les entités par seconde ?](#subheading24) |
| &nbsp; | Tables |Configuration |[Utilisez-vous JSON pour vos demandes de table ?](#subheading25) |
| &nbsp; | Tables |Configuration |[Avez vous désactivé Nagle tooimprove les performances de hello de petites requêtes ?](#subheading26) |
| &nbsp; | Tables |Tables et partitions |[Avez-vous correctement partitionné vos données ?](#subheading27) |
| &nbsp; | Tables |Partitions actives |[Évitez-vous les modèles « Ajouter après uniquement » ou « Ajouter avant uniquement » ?](#subheading28) |
| &nbsp; | Tables |Partitions actives |[Vos opérations d'insertion/de mise à jour couvrent-elles plusieurs partitions ?](#subheading29) |
| &nbsp; | Tables |Étendue de requête |[Avez conçu votre tooallow de schéma pour le point de requêtes toobe est utilisé dans la plupart des cas et toobe de requêtes de table utilisée avec parcimonie ?](#subheading30) |
| &nbsp; | Tables |Densité des requêtes |[En règle générale, vos requêtes n'analysent et ne renvoient-elles que les lignes qui seront utilisées par votre application ?](#subheading31) |
| &nbsp; | Tables |Limitation des données renvoyées |[Vous utilisez le filtrage tooavoid retournant des entités qui ne sont pas nécessaires ?](#subheading32) |
| &nbsp; | Tables |Limitation des données renvoyées |[Vous utilisez tooavoid projection retourner des propriétés qui ne sont pas nécessaires ?](#subheading33) |
| &nbsp; | Tables |Dénormalisation |[Avoir dénormalisée vos données telles que vous évitez des requêtes inefficaces ou plusieurs demandes de lecture lors de la tentative de tooget données ?](#subheading34) |
| &nbsp; | Tables |Insertion/Mise à jour/Suppression |[Sont vous le traitement par lot les demandes qui doivent toobe transactionnelle ou peuvent être effectuées à hello même tooreduce allers-retours de temps ?](#subheading35) |
| &nbsp; | Tables |Insertion/Mise à jour/Suppression |[Sont éviter la récupération d’un toodetermine simplement entité si toocall insérer ou mettre à jour ?](#subheading36) |
| &nbsp; | Tables |Insertion/Mise à jour/Suppression |[Avez-vous envisagé de stocker des séries de données qui seront fréquemment récupérées ensemble dans une seule entité sous la forme de propriétés plutôt que d'entités multiples ?](#subheading37) |
| &nbsp; | Tables |Insertion/Mise à jour/Suppression |[Dans le cas des tables qui sont toujours récupérées ensemble et qui peuvent être écrites par lots (des données de séries temporelles, par exemple), avez-vous envisagé d'utiliser des objets blob à la place de tables ?](#subheading38) |
| &nbsp; | Files d’attente |Objectifs d'évolutivité |[Sont vous approchant hello objectifs d’évolutivité pour les messages par seconde ?](#subheading39) |
| &nbsp; | Files d’attente |Configuration |[Avez vous désactivé Nagle tooimprove les performances de hello de petites requêtes ?](#subheading40) |
| &nbsp; | Files d’attente |Taille des messages |[Sont des performances de hello tooimprove compact de file d’attente hello vos messages ?](#subheading41) |
| &nbsp; | Files d’attente |Récupération en bloc |[Récupérez-vous plusieurs messages dans une seule opération « Get » ?](#subheading42) |
| &nbsp; | Files d’attente |Fréquence d'interrogation |[Vous demandent souvent assez hello tooreduce la perception de la latence de votre application ?](#subheading43) |
| &nbsp; | Files d’attente |Mise à jour de message |[Vous utilisez UpdateMessage toostore progression dans le traitement des messages, en évitant d’avoir le message entier de type hello tooreprocess si une erreur se produit ?](#subheading44) |
| &nbsp; | Files d’attente |Architecture |[Vous utilisez les files d’attente toomake toute votre application plus évolutive en conservant les charges de travail de longue hors critique hello et l’échelle puis indépendamment ?](#subheading45) |

## <a name="allservices"></a>Tous les Services
Cette section répertorie les pratiques qui sont applicables toohello aucune utilisation de services de stockage Azure hello (objets BLOB, tables, files d’attente ou fichiers).  

### <a name="subheading1"></a>Objectifs d’extensibilité
Chacun des services de stockage Azure hello a les objectifs d’évolutivité de capacité (Go), taux de transactions et la bande passante. Si votre application est proche ou dépasse les objectifs d’évolutivité hello, il peut rencontrer des temps de latence accrue des transactions ou de limitations. Lorsqu’un service de stockage limite votre application, service de hello commence tooreturn « 503 serveur occupé » ou « délai d’attente de 500 opération » codes d’erreur pour certaines transactions de stockage. Cette section décrit les deux toodealing approche générale de hello avec les objectifs d’évolutivité et les objectifs d’évolutivité de la bande passante en particulier. Les sections suivantes qui traitent des services de stockage individuel discuter des objectifs d’extensibilité dans le contexte de hello de ce service spécifique :  

* [Bande passante des objets blob et demandes par seconde](#subheading16)
* [Entités de table par seconde](#subheading24)
* [Messages de file d’attente par seconde](#subheading39)  

#### <a name="sub1bandwidth"></a>Cible d’extensibilité de bande passante pour tous les services
Au moment de l’écriture de hello, cibles de la bande passante hello dans le compte de hello US pour un stockage géo-redondant (GRS) sont 10 gigabits par seconde (Gbits/s) pour l’entrée (données envoyées de compte de stockage toohello) et 20 Gbits/s pour la sortie (les données envoyées à partir du compte de stockage hello). Pour un compte de stockage localement redondant (LRS), les limites de hello sont supérieurs – 20 Gbits/s pour l’entrée et de 30 Gbits/s pour les sorties.  Les limites de bande passante internationales peuvent être inférieures. Pour les consulter, rendez-vous sur la [page traitant des objectifs d’extensibilité](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Pour plus d’informations sur les options de redondance de stockage hello, consultez les liens de hello dans [ressources utiles](#sub1useful) ci-dessous.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>Le toodo lors de l’approche d’une cible d’évolutivité
Si votre application est proche des objectifs d’évolutivité hello pour un seul compte de stockage, envisager d’adopter une des méthodes suivantes de hello :  

* Reconsidérer la charge de travail hello provoque tooapproach de votre application ou dépasser hello évolutivité cible. Pourrez vous la concevez différemment toouse moins de bande passante ou de capacité ou moins de transactions ?
* Si une application doit dépasser la valeur d’un des objectifs d’évolutivité hello, vous devez créer plusieurs comptes de stockage et la partition vos données d’application sur ces plusieurs comptes de stockage. Si vous utilisez ce modèle, puis être toodesign que votre application afin que vous pouvez ajouter plusieurs comptes de stockage Bonjour future pour l’équilibrage de charge. Au moment de l’écriture, chaque abonnement Azure peut avoir des comptes de stockage too100.  De plus, aucun coût autre que l’utilisation en termes de données stockées, de transactions effectuées ou de données transférées n’est associé à ces comptes de stockage.
* Si votre application rencontre des cibles de la bande passante hello, envisagez la compression des données dans hello client tooreduce hello la bande passante requise toosend hello toohello stockage service de données.  Bien que cela puisse réduire la bande passante et améliorer les performances du réseau, cette méthode présente des aspects négatifs.  Vous devez évaluer l’impact sur les performances hello de cette échéance toohello les exigences de traitement supplémentaires pour compresser et décompresser les données hello client. En outre, le stockage des données compressées peut rendre plus difficile tootroubleshoot problèmes dans la mesure où il peut s’agir des données tooview stockée plus difficiles à l’aide d’outils standard.
* Si votre application rencontre des objectifs d’évolutivité hello, assurez-vous que vous utilisez une interruption exponentielle des nouvelles tentatives (consultez [tentatives](#subheading14)).  Ses meilleures toomake que vous approche jamais les objectifs d’évolutivité hello (en utilisant une des hello au-dessus de méthodes), mais cela permet de garantir votre application ne sera pas simplement une nouvelle tentative rapidement, rendre hello pire de limitation.  

#### <a name="useful-resources"></a>Ressources utiles
Hello suivant liens fournit des détails supplémentaires sur les objectifs d’évolutivité :

* Pour plus d’informations sur les objectifs d’extensibilité, consultez [Objectifs de performance et évolutivité d’Azure Storage](storage-scalability-targets.md) .
* Consultez [réplication de stockage Azure](storage-redundancy.md) et le billet de blog hello [Options de redondance de stockage Azure et Read Access Geo Redundant Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) pour plus d’informations sur les options de redondance de stockage.
* Pour obtenir des informations à jour sur la tarification des services Azure, consultez la page [Tarification Azure](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>Conventions d’affectation de noms aux partitions
Le stockage Azure utilise un basée sur une plage partitionnement schéma tooscale et charge solde hello système. clé de partition Hello est données toopartition utilisés dans les plages et ces plages sont équilibrées entre le système de hello. Cela signifie que les conventions d’affectation de noms tels que lexicale de classement (par exemple, msftpayroll, msftperformance, msftemployees, etc.) ou d’à l’aide d’un horodatage (log20160101, log20160102, log20160102, etc.) seront prête partitions toohello étant potentiellement COLOCALISÉES sur hello même serveur de partition, jusqu'à ce qu’une opération d’équilibrage de charge les fractionne en plus petites plages. Par exemple, tous les objets BLOB dans un conteneur peuvent être pris en charge par un seul serveur jusqu'à ce que hello charge sur ces objets BLOB ne nécessite plus le rééquilibrage des plages de partition hello. De même, un groupe de comptes légèrement chargés avec leurs noms organisés dans l’ordre lexical peut-être être traité par un seul serveur jusqu'à ce que hello charger sur l’un ou de tous ces comptes ont besoin toobe fractionné entre plusieurs serveurs de partitions. Chaque opération d’équilibrage de charge peut affecter la latence hello d’appels de stockage au cours de l’opération de hello. toohandle de capacité du système Hello qu'une soudaine de la partition de tooa le trafic est limitée par hello d’un serveur de partition unique jusqu'à ce que l’opération d’équilibrage de charge hello intervient dans et rééquilibrage de plage de clés de partition hello.  

Vous pouvez suivre certaines fréquence de hello de tooreduce meilleures pratiques de ces opérations.  

* Examinez la convention de dénomination hello qu'utiliser des comptes, conteneurs, objets BLOB, tables et files d’attente, en étroite collaboration. Vous pouvez ajouter un préfixe aux noms de comptes avec un hachage à 3 chiffres à l'aide d'une fonction de hachage qui correspond le mieux à vos besoins.  
* Si vous organisez vos données à l’aide d’horodatages ou les identificateurs numériques, vous avez tooensure vous n’utilisez pas un trafic ajout uniquement (ou ajouter avant uniquement). Ces modèles ne conviennent pas pour une plage de-en fonction de partitionnement du système, et pourraient prospect tooall hello le trafic continu tooa unique partition et limitation système hello à partir d’efficacement l’équilibrage de charge. Par exemple, si vous disposez de tous les jours les opérations qui utilisent un objet blob avec un horodateur tel qu’AAAAMMJJ, puis hello trafic pour que l’opération quotidienne est dirigé tooa seul objet est pris en charge par un seul serveur de partitions. Regardez si hello par l’objet blob de limite et par partition limites répondent à vos besoins et arrêtez cette opération en plusieurs objets BLOB si nécessaire. De même, si vous stockez des données de série chronologique dans vos tables, tout le trafic de hello peut être dirigé toohello dernière partie de l’espace de noms clé hello. Si vous devez utiliser les horodatages ou les ID numériques, préfixe id hello avec un code de hachage à 3 chiffres ou, dans les cas de hello partie horodateurs préfixe hello secondes de temps hello telles que ssyyyymmdd. Si des opérations de listage et d'interrogation sont effectuées régulièrement, choisissez une fonction de hachage qui limite le nombre de vos requêtes. Dans d'autres cas, un préfixe aléatoire peut être suffisant.  
* Pour plus d’informations sur hello utilisé dans le stockage Azure de schéma de partitionnement, lire le document du sosp sur Microsoft hello [ici](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Mise en réseau
Tandis que hello API appelle question, souvent les contraintes de réseau physique hello de l’application hello ont un impact significatif sur les performances. suivant de Hello décrire certaines des limitations, les utilisateurs peuvent rencontrer.  

#### <a name="client-network-capability"></a>Fonctionnalités réseau du client
##### <a name="subheading2"></a>Débit
Pour la bande passante, problème de hello est souvent hello fonctionnalités de hello client. Par exemple, si un seul compte de stockage peut gérer au moins 10 Gbits/s en entrée (consultez [objectifs d’évolutivité de la bande passante](#sub1bandwidth)), la vitesse réseau hello dans une instance de rôle de travail Azure « Petite » n’est capable d’environ 100 Mbits/s. Dans le cas des instances Azure plus importantes, les cartes réseau présentent une capacité supérieure. Si vous avez besoin de limites réseau plus élevées à partir d’un seul ordinateur, vous devez donc envisager d’utiliser une instance plus grande ou davantage de machines virtuelles. Si vous accédez à un service de stockage à partir d’une application de site sur, puis hello même règle s’applique : comprendre les capacités de réseau hello de périphérique de client hello et toohello de connectivité réseau hello emplacement de stockage Azure et l’améliorer en fonction des besoins ou concevoir votre toowork d’application au sein de leurs fonctionnalités.  

##### <a name="subheading3"></a>Qualité de la liaison
Comme c’est le cas pour toute utilisation du réseau, veuillez tenir compte du fait que les conditions réseau qui génèrent des erreurs et une perte de paquets ralentissent le débit effectif.  L’utilisation de WireShark ou de NetMon peut vous aider à diagnostiquer ce problème.  

##### <a name="useful-resources"></a>Ressources utiles
Pour plus d’informations sur les tailles de machines virtuelles et la bande passante allouée, consultez la rubrique [Tailles des machines virtuelles](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Tailles des machines virtuelles Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Emplacement
Dans un environnement distribué, placer client hello proximité toohello serveur remet dans les meilleurs hello. Pour accéder à Azure Storage avec une latence plus faible hello, hello meilleur emplacement pour votre client se trouve dans hello même région Azure. Par exemple, dans le cas d’un site web qui utilise Azure Storage, tous deux doivent se trouver dans la même région (Ouest des États-Unis ou Asie du Sud-Est, par exemple). Cela réduit la latence hello et hello coût : au moment de l’écriture de hello, l’utilisation de la bande passante dans une région est gratuite.  

Si votre client applications ne sont pas hébergées dans Azure (tels que des applications pour appareil mobile ou sur les services d’entreprise local), puis à nouveau placer le compte de stockage hello dans une région proche toohello les appareils qui s’y accéder, généralement réduira la latence. En cas de distribution à grande échelle de vos clients (par exemple, certains se trouvent en Amérique du Nord et d’autres en Europe), l’utilisation de plusieurs comptes de stockage peut s’avérer judicieuse : un dans une région de l’Amérique du Nord et l’autre dans une région d’Europe. Cela permet de latence tooreduce pour les utilisateurs dans les deux régions. Cette approche est généralement plus facile tooimplement si hello hello application banques de données des utilisateurs tooindividual spécifique et ne nécessite pas de réplication de données entre des comptes de stockage.  Pour une large distribution de contenu, un CDN est recommandé : consultez hello la section suivante pour plus d’informations.  

### <a name="subheading5"></a>Distribution de contenu
Parfois, un hello tooserve de besoins application même contenu réduire utilisateurs (par exemple, un produit démonstration vidéo utilisé dans la page d’accueil hello d’un site Web), situé dans le hello même ou plusieurs régions. Dans ce scénario, vous devez utiliser un réseau de distribution contenu (CDN) tels que Azure CDN et hello CDN utiliserait le stockage Azure en tant qu’origine hello de données de hello. Contrairement à un compte de stockage Azure qui existe dans une région et qui ne peut pas fournir du contenu avec une faible latence tooother régions, CDN Azure utilise des serveurs dans plusieurs centres de données Bonjour. De plus, un CDN peut généralement prendre en charge des limites de sortie bien plus élevées qu’un compte de stockage unique.  

Pour plus d’informations sur le CDN Azure, voir la page [CDN Azure](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>Utilisation de SAP et de CORS
Lorsque vous avez besoin de code tooauthorize tels que JavaScript dans le navigateur web d’un utilisateur ou un téléphone mobile de données de tooaccess application dans le stockage Azure, une approche consiste à toouse une application dans un rôle web en tant que proxy : périphérique hello de l’utilisateur s’authentifie avec un rôle web de hello, qui à son tour authentifie avec le service de stockage hello. Vous évitez ainsi d’exposer vos clés de compte de stockage sur des appareils non sécurisés. Toutefois, il s’ensuit une charge importante sur le rôle web de hello, car toutes les données de hello transférées entre le périphérique de l’utilisateur hello et service de stockage hello doit passer par le rôle web de hello. Vous pouvez éviter d’utiliser un rôle web en tant que proxy pour le service de stockage hello par à l’aide d’accès partagé des Signatures (SAS), parfois en association avec des en-têtes de partage des ressources Cross-Origin (CORS). À l’aide de SAP, vous pouvez autoriser que toomake de périphérique de l’utilisateur de votre demande directement tooa stockage de service au moyen d’un jeton d’accès limité. Par exemple, si un utilisateur souhaite tooupload une application de tooyour photo, votre rôle web peut générer et envoyer de périphérique de l’utilisateur toohello un jeton SAS qui autorise l’objet blob d’autorisation toowrite tooa spécifique ou un conteneur pour hello suivants 30 minutes (après quoi hello jeton SAS expire).

Normalement, un navigateur ne permet pas de JavaScript dans une page hébergée par un site Web sur un seul tooperform des opérations spécifiques de domaine comme un domaine tooanother « PUT ». Par exemple, si vous hébergez un rôle web à « contosomarketing.cloudapp.net » et que vous souhaitez toouse client côté JavaScript tooupload un compte de stockage blob tooyour à « contosoproducts.blob.core.windows.net », hello du navigateur « stratégie d’origine » sera c’est impossible opération. CORS est une fonctionnalité de navigateur qui permet de hello domaine (dans ce compte de stockage cas hello) toocommunicate toohello navigateur cible qu’il approuve les demandes provenant de domaine source de hello (dans ce rôle web de cas hello).  

Ces deux technologies vous aident à éviter toute charge inutile (ainsi que les goulots d’étranglement) au niveau de votre application web.  

#### <a name="useful-resources"></a>Ressources utiles
Pour plus d’informations sur SAS, consultez [Signatures d’accès partagé, partie 1 : hello de présentation modèle SAP](../storage-dotnet-shared-access-signature-part-1.md).  

Pour plus d’informations sur CORS, consultez [prise en charge de partage de ressources Cross-Origin (CORS) pour hello Services de stockage Azure](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Mise en cache
#### <a name="subheading7"></a>Récupération de données
En règle générale, il est préférable de récupérer des données d’un service à une seule reprise plutôt que deux fois. Envisagez un exemple hello d’application web MVC en cours d’exécution dans un rôle web qui a déjà récupéré un objet blob de 50 Mo tooserve de service de stockage hello en tant qu’utilisateur de contenu tooa. application Hello pu puis récupérer ce même objet blob chaque fois qu’un utilisateur le demande, ou il peut mettre en cache localement toodisk et réutilisation version mise en cache hello pour les demandes suivantes des utilisateurs. En outre, chaque fois qu’un utilisateur demande des données de hello, hello application pu émettre GET avec un en-tête conditionnel pour l’heure de modification et serait éviter d’obtenir des objets blob de la totalité de hello s’il n’a pas été modifié. Vous pouvez appliquer cette même tooworking de modèle avec les entités de table.  

Dans certains cas, vous pouvez décider que votre application peut assumer que ce blob hello reste valide pendant une courte période après la récupération, et que pendant cette période hello application n’a pas besoin toocheck si l’objet blob de hello a été modifié.

Configuration, de recherche et d’autres données qui sont toujours utilisées par l’application hello sont des candidats idéaux pour la mise en cache.  

Pour obtenir un exemple de comment tooget hello de toodiscover de propriétés d’un objet blob date de dernière modification à l’aide de .NET, consultez [ensemble et récupérer des propriétés et métadonnées](../blobs/storage-properties-metadata.md). Pour plus d’informations sur les téléchargements conditionnels, consultez [Spécification d’en-têtes conditionnels pour les opérations de Service Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Téléchargement de données par lots
Dans certains scénarios d’application, vous pouvez agréger des données en local, puis les télécharger périodiquement dans un lot au lieu de les télécharger immédiatement une à une. Par exemple, une application web peut conserver un fichier journal des activités : hello application pourrait soit télécharger des détails de chaque activité comme il se produit comme une entité de table (qui nécessite de nombreuses opérations de stockage), ou il peut enregistrer des détails tooa local fichier journal d’activité, puis Télécharger régulièrement tous les détails de l’activité en tant qu’un objet blob tooa de fichier délimité. Si la taille est 1 Ko pour chaque entrée de journal, vous pouvez télécharger des milliers dans une seule transaction « Put Blob » (vous pouvez télécharger un objet blob de configuration too64MB taille dans une transaction unique). Bien entendu, en cas de hello local toohello préalable téléchargement vous serez de perdre des données de journal : développeur d’applications hello doit concevoir possibilité hello de périphérique client ou télécharger des échecs.  Si les données d’activité hello doivent toobe téléchargé pour les intervalles de temps (pas juste une activité), les objets BLOB est recommandés sur des tables.

### <a name="net-configuration"></a>Configuration .NET
Si à l’aide de hello .NET Framework, cette section répertorie plusieurs paramètres de configuration rapide que vous pouvez utiliser les améliorations significatives des performances de toomake.  Si vous utilisez d’autres langages, vérifiez toosee si les concepts similaires s’appliquent dans le langage choisi.  

#### <a name="subheading9"></a>Augmentation de la limite de connexions par défaut
Dans .NET, hello suivant code augmente la limite de connexion par défaut hello (qui est généralement 2 dans un environnement client ou 10 dans un environnement de serveur) too100. En règle générale, vous devez définir nombre de hello hello valeur tooapproximately de threads utilisés par votre application.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

Vous devez définir le nombre maximal de connexions hello avant l’ouverture de toutes les connexions.  

Pour les autres langages de programmation, consultez toodetermine de documentation de ce langage comment limiter les connexions de hello tooset.  

Pour plus d’informations, voir blog de hello [Services Web : connexions simultanées](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>Augmentation du nombre minimum de threads du pool de threads en cas d’utilisation de code synchrone avec Async Tasks
Ce code augmentera hello min threads du pool :  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Pour plus d’informations, consultez [Méthode ThreadPool.SetMinThreads](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>Utilisation du nettoyage de la mémoire de .NET 4.5
Utiliser .NET 4.5 ou version ultérieure pour hello client application tootake un avantage des améliorations de performances de garbage collection côté serveur.

Pour plus d’informations, voir l’article hello [une vue d’ensemble d’améliorations des performances dans .NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Parallélisme illimité
Alors que le parallélisme peut être intéressante pour les performances, veillez à plusieurs partitions à l’aide de parallélisme unbounded (aucune limite sur nombre hello de threads et/ou les demandes parallèles) tooupload ou télécharger des données, à l’aide de plusieurs threads de travail tooaccess (conteneurs, des files d’attente, ou partitions de table) dans hello même compte de stockage ou tooaccess plusieurs éléments Bonjour même partition. Si le parallélisme de hello est illimité, votre application peut dépasser les capacités du périphérique hello client ou hello objectifs d’évolutivité du compte de stockage entraîne plus élevés et de limitation.  

### <a name="subheading13"></a>Outils et bibliothèques clientes de stockage
Toujours utiliser les outils et bibliothèques de client hello dernière fournis par Microsoft. Au moment de hello d’écriture, il existe des bibliothèques clientes disponibles pour .NET, Windows Phone, Windows Runtime, Java et C++, ainsi que les bibliothèques d’aperçu pour d’autres langues. Microsoft a, en outre, publié des cmdlets PowerShell et des commandes de l’interface de ligne de commande, utilisables avec Azure Storage. Microsoft activement développe ces outils avec des performances à l’esprit les maintient des toodate avec les dernières versions de service hello et permet de s’assurer qu’ils gèrent de nombreux hello éprouvée pratiques de performance en interne.  

### <a name="retries"></a>Nouvelle tentatives
#### <a name="subheading14"></a>Limitation/Serveur occupé
Dans certains cas, hello service de stockage peut limiter votre application ou peut simplement être demande de hello tooserve impossible en raison de conditions transitoires de toosome et renvoyer un message « 503 serveur occupé » ou « Timeout 500 ».  Cela peut se produire si un des objectifs d’évolutivité hello est proche de votre application, ou si le système de hello est rééquilibrage votre tooallow les données partitionnées pour un débit plus élevé.  application cliente de Hello doit généralement retenter hello qui provoque cette erreur : tentative de hello même demande plus tard peut réussir. Toutefois, si le service de stockage hello est la limitation de votre application, car il dépasse les objectifs d’évolutivité, ou même si le service de hello était demande de hello tooserve Impossible pour une raison quelconque, des tentatives d’agressives généralement aggraver hello problème. Pour cette raison, vous devez utiliser une valeur exponentielle hors tension (hello client bibliothèques toothis par défaut). Votre application peut, par exemple, effectuer une nouvelle tentative après 2 secondes, puis 4 secondes, 10 secondes, 30 secondes avant d’abandonner complètement. Ce comportement provoque votre application considérablement réduire la charge sur le service de hello plutôt qu’exacerber les problèmes.  

Notez que les erreurs de connectivité peuvent être retentées immédiatement, car ils ne sont pas des résultats hello de limitation et sont attendu toobe temporaire.  

#### <a name="subheading15"></a>Erreurs non renouvelables
les bibliothèques clientes Hello connaissent les erreurs sont en mesure de nouvelle tentative et qui ne sont pas. Toutefois, si vous écrivez votre propre code contre le stockage hello API REST, n’oubliez pas de certaines erreurs qui vous ne convient pas de nouvelle tentative : par exemple, un 400 (demande incorrecte) réponse indique l’application hello client a envoyé une demande qui ne peut pas être traitée car elle n’était pas dans un format attendu. Renvoi de cette demande entraîne hello même réponse chaque fois, donc il est inutile de nouvelle tentative il. Si vous écrivez votre propre code contre le stockage hello API REST, tenez compte des codes d’erreur hello moyenne et hello tooretry de manière appropriée (ou pas) pour chacun d’eux.  

#### <a name="useful-resources"></a>Ressources utiles
Pour plus d’informations sur les codes d’erreur de stockage, consultez [d’état et Codes d’erreur](http://msdn.microsoft.com/library/azure/dd179382.aspx) sur le site web de Microsoft Azure hello.  

## <a name="blobs"></a>Objets blob
Dans toohello plus pratiques pour éprouvées [tous les Services](#allservices) décrit précédemment, suivant hello pratiques éprouvées s’appliquent en particulier le service de blob toohello.  

### <a name="blob-specific-scalability-targets"></a>Objectifs d’extensibilité propres aux objets blob
#### <a name="subheading46"></a>Plusieurs clients accédant simultanément à un seul objet
Si vous avez un grand nombre de clients accèdent simultanément à un objet unique, vous devez tooconsider par objet et stockage cibles d’extensibilité de compte. nombre exact de Hello de clients qui peuvent accéder à un objet unique sera varient en fonction de facteurs tels que nombre hello de clients demandant des objets de hello simultanément, taille hello d’objet de hello, etc. de conditions réseau.

Si l’objet de hello peut être distribué via un réseau CDN comme des images ou vidéos pris en charge à partir d’un site Web, puis vous devez utiliser un CDN. Voir [ici](#subheading5).

Dans d’autres scénarios, telles que des simulations scientifiques où les données de salutation sont confidentielles, vous avez deux options. Hello est tout d’abord toostagger access de votre charge de travail telle que hello objet est accédé sur une période de vs de temps en cours d’accès simultanément. Ou bien, vous pouvez copier temporairement les comptes de stockage toomultiple objet hello améliorant hello total IOPS par objet et sur les comptes de stockage. Dans limitées de test, nous avons trouvé qu’environ 25 ordinateurs virtuels peuvent télécharger simultanément un objet blob de 100 Go en parallèle (chaque machine virtuelle a été parallélisation téléchargement hello à l’aide de 32 threads). Si vous aviez 100 clients nécessitant l’objet de hello tooaccess, tout d’abord copier tooa deuxième compte de stockage ont hello 50 premiers ordinateurs virtuels accès hello premier objet blob et hello ensuite 50 ordinateurs virtuels accès hello deuxième objet blob. Les résultats varient selon le comportement de vos applications. Nous vous conseillons de tester ceci pendant la conception. 

#### <a name="subheading16"></a>Bande passante et opérations par objet blob
Vous pouvez lire ou écrire tooa unique objet blob à des tooa jusqu'à 60 Mo par seconde (il s’agit d’environ 480 Mbits/s qui dépasse les capacités de hello de nombreux réseaux du côté client (y compris de hello carte réseau physique sur le périphérique de client hello). En outre, un seul objet blob prend en charge les demandes de too500 par seconde. Si vous avez plusieurs clients qui ont besoin de tooread hello même objet blob et que vous pouvez dépasse ces limites, vous devez envisager d’utiliser un CDN pour distribuer des objets blob de hello.  

Pour plus d’informations sur le débit cible pour les objets blob, consultez [Objectifs de performance et d’extensibilité d’Azure Storage](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Copie et déplacement d’objets blob
#### <a name="subheading17"></a>Copie d’un objet blob
stockage de Hello version 2012-02-12 de l’API REST introduites toocopy objets BLOB de la capacité utile hello sur plusieurs comptes : une application cliente peut demander à toocopy de service de stockage hello un objet blob à partir d’une autre source (éventuellement dans un autre compte de stockage) et le laisser hello service copier hello en mode asynchrone. Cela peut réduire considérablement la bande passante hello nécessaire pour l’application hello lorsque vous avez une migration des données à partir d’autres comptes de stockage, car vous ne pas besoin toodownload et télécharger les données de salutation.  

Tenez compte notamment, toutefois, est que, lors de la copie entre des comptes de stockage, il n’existe aucune garantie de temps sur lorsque la copie de hello s’achève. Si votre application doit toocomplete un objet blob copier rapidement sous votre contrôle, il peut être une meilleure blob de hello toocopy en téléchargeant tooa machine virtuelle, puis téléchargez toohello destination.  Prévisibilité complète dans ce cas, assurez-vous que la copie de hello est effectuée par un ordinateur virtuel en cours d’exécution dans hello même région Azure, ou bien les conditions du réseau peut (et sera probablement) affectent les performances de la copie.  En outre, vous pouvez évaluer les progrès hello d’une copie asynchrone par programme.  

Notez que le copie dans hello même compte de stockage se sont terminées généralement rapidement.  

Pour plus d’informations, consultez [Copie d’un objet blob](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>Utilisation d’AzCopy
équipe du stockage Azure Hello a publié un outil de ligne de commande « AzCopy » qui est revient toohelp en transfert de nombreux objets BLOB à, à partir d’et sur les comptes de stockage de masse.  Cet outil est optimisé pour ce scénario et peut générer des taux de transfert élevés.  Il est vivement conseillé de l’utiliser pour les opérations de chargement, de téléchargement et de copie en bloc. toolearn plus d’informations et le télécharger, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Service Azure Import/Export
Pour les très grands volumes de données (plus de 1 To), hello Azure Storage offre hello service Import/Export, ce qui permet de chargement et le téléchargement à partir du stockage d’objets blob par envoi de journaux des disques durs.  Vous pouvez placer vos données sur un disque dur et envoyez-le tooMicrosoft pour le téléchargement ou envoyer un disque dur vide tooMicrosoft toodownload de données.  Pour plus d’informations, consultez [utiliser hello Service Microsoft Azure Import/Export tooTransfer données tooBlob stockage](../storage-import-export-service.md).  Cela peut être beaucoup plus efficace que du téléchargement ce volume de données sur le réseau de hello.  

### <a name="subheading20"></a>Utilisation de métadonnées
service d’objets blob Hello prend en charge les demandes head, qui peuvent inclure des métadonnées sur l’objet blob de hello. Par exemple, si votre application nécessaire données EXIF hello une photo, il pourrait extraire photo de hello et extrayez-le. la bande passante toosave et améliorer les performances, votre application peut stocker des données EXIF de hello dans les métadonnées de l’objet blob de hello lors de l’application hello téléchargé photo de hello : vous pouvez ensuite récupérer les données EXIF hello dans les métadonnées à l’aide uniquement d’une demande HEAD, l’enregistrement d’une bande passante et le temps de traitement hello tooextract hello données EXIF chaque objet blob hello de temps est en lecture est nécessaire. Il serait utile dans les scénarios où vous devez uniquement les métadonnées hello et pas hello contenu complet d’un objet blob.  Notez qu’uniquement 8 Ko de métadonnées peuvent être stockée par l’objet blob (hello service acceptera pas une demande toostore supérieure), donc si les données de salutation ne tient pas dans cette taille, vous ne pouvez pas être en mesure de toouse cette approche.  

Pour obtenir un exemple de procédure tooget les métadonnées d’un objet blob à l’aide de .NET, consultez [ensemble et récupérer des propriétés et métadonnées](../blobs/storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Téléchargement rapide
objets BLOB tooupload rapide, est de hello première question tooanswer : vous êtes téléchargement d’un objet blob ou nombreux ?  Utilisez hello ci-dessous les conseils toodetermine hello méthode correcte toouse selon votre scénario.  

#### <a name="subheading21"></a>Téléchargement rapide d’un objet blob volumineux
tooupload un seul grand blob rapidement, votre application cliente doit télécharger ses blocs ou les pages en parallèle (penser objectifs d’évolutivité hello pour les objets BLOB individuels et le compte de stockage hello dans son ensemble en cours).  Notez que hello officiel fournie par Microsoft RTM stockage bibliothèques clientes (.NET, Java) hello capacité toodo cela.  Pour chacune des bibliothèques de hello, utilisez hello seuil spécifié/propriété de l’objet tooset hello d’accès concurrentiel :  

* .NET : ParallelOperationThreadCount d’ensemble sur un toobe d’objet BlobRequestOptions utilisé.
* Java/Android : utilisez BlobRequestOptions.setConcurrentRequestCount()
* Node.js : Utilisez parallelOperationThreadCount sur les deux options de demande hello ou service d’objets blob hello.
* C++ : Utilisez la méthode blob_request_options::set_parallelism_factor de hello.

#### <a name="subheading22"></a>Téléchargement rapide de nombreux objets blob
tooupload grand nombre d’objets BLOB rapidement, télécharger des objets BLOB en parallèle. Il est plus rapide que le chargement des objets BLOB unique à la fois avec les téléchargements de bloc parallèle, car il répartit hello téléchargement sur plusieurs partitions hello du service de stockage. Dans le cas d’un objet blob unique, le débit pris en charge est seulement de 60 Mo/seconde (environ 480 Mbits/s). Au moment de l’écriture de hello, un compte LRS de basés aux États-Unis prend en charge jusqu'à too20 entrée Gbits/s qui est beaucoup plus que le débit hello pris en charge par un objet blob individuel.  [AzCopy](#subheading18) effectue des téléchargements en parallèle et son utilisation est recommandée pour ce scénario.  

### <a name="subheading23"></a>Choix d’objets blob correct de type hello
Azure Storage prend en charge deux types d’objet blob : *de pages* et *de blocs*. Pour un scénario donné, le choix du type d’objet blob affectera les performances hello et l’évolutivité de votre solution. Objets BLOB de blocs est appropriés lorsque vous souhaitez qu’efficacement tooupload grandes quantités de données : par exemple, une application cliente peut-être les photos tooupload ou vidéo tooblob stockage. Objets BLOB de pages est approprié si l’application hello doit tooperform des écritures aléatoires sur les données de salutation : par exemple, les disques durs virtuels de Azure sont stockés en tant qu’objets BLOB de pages.  

Pour plus d’informations, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tables
Dans toohello plus pratiques pour éprouvées [tous les Services](#allservices) décrit précédemment, suivant hello pratiques éprouvées s’appliquent en particulier le service de table toohello.  

### <a name="subheading24"></a>Objectifs d’extensibilité propres aux tables
Dans les limitations de bande passante plus toohello d’un compte de stockage dans son intégralité, les tables ont hello suivant limite d’évolutivité spécifique.  Notez que le système de hello équilibre la charge en tant que votre augmente le trafic, mais si votre trafic possède des rafales soudaines, vous ne pouvez pas être en mesure de tooget ce volume de débit d’immédiatement.  Si votre modèle a des pics d’activité, vous devriez toosee limitation et/ou des délais d’attente pendant hello rafale en tant que service de stockage hello automatiquement équilibre la charge de votre table.  En identifiant lentement généralement a meilleurs résultats, car il fournit solde de tooload de temps système hello de manière appropriée.  

#### <a name="entities-per-second-account"></a>Entités par seconde (compte)
limite d’évolutivité Hello pour l’accès aux tables est too20, 000 entités (1 Ko) par seconde pour un compte.  En règle générale, chaque entité insérée, mise à jour, supprimée ou analysée est comptabilisée.  Une insertion par lots composée de 100 entités compte donc pour 100 entités.  De même, une requête qui analyse 1 000 entités et en renvoie 5 compte pour 1 000 entités.  

#### <a name="entities-per-second-partition"></a>Entités par seconde (partition)
Dans une même partition, hello cible d’évolutivité pour l’accès aux tables d’est 2 000 entités (1 Ko) par seconde, à l’aide de hello comptage même comme décrit dans la section précédente de hello.  

### <a name="configuration"></a>Configuration
Cette section répertorie plusieurs paramètres de configuration rapide que vous pouvez utiliser des améliorations significatives des performances de toomake hello service de table :  

#### <a name="subheading25"></a>Utilisation de JSON
Depuis la version de service de stockage 2013-08-15, service de table hello prend en charge l’utilisation de JSON au lieu du format de basé sur XML de AtomPub hello pour le transfert de données de la table. Cela peut réduire la taille de la charge utile de 75 % et peut améliorer considérablement les performances de hello de votre application.

Pour plus d’informations, consultez hello [les Tables Microsoft Azure : présentation de JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) et [Format de charge utile pour les opérations de Service de Table](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Désactivation de Nagle
Algorithme de Nagle est largement implémenté sur les réseaux TCP/IP moyens tooimprove des performances réseau. Cependant, il n’est pas idéal dans toutes les situations (c’est le cas, par exemple, dans les environnements très interactifs). Pour le stockage Azure, algorithme de Nagle a un impact négatif sur les performances de hello de demandes toohello table et file d’attente des services, et vous devez la désactiver si possible.  

Pour plus d’informations, voir notre blog [algorithme du Nagle n’est pas convivial aux petites requêtes](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), qui explique pourquoi algorithme de Nagle interagit mal avec les requêtes de table et de la file d’attente et montre comment toodisable dans votre client application.  

### <a name="schema"></a>Schéma
Utilisation de représenter et d’interroger vos données est hello plus un facteur qui affecte les performances de hello du service de table hello. Bien que chaque application soit différente, cette section énumère quelques pratiques générales concernant les points suivants :  

* Conception de tables
* Requêtes efficaces
* Mises à jour de données efficaces  

#### <a name="subheading27"></a>Tables et partitions
Les tables sont divisées en partitions. Chaque entité stocké dans une partition partages hello la même clé de partition et a un tooidentify de clé de ligne unique dans cette partition. Les partitions offrent des avantages, mais elles s’accompagnent également de limites d’extensibilité.  

* Avantages : Vous pouvez mettre à jour les entités Bonjour même partition dans une transaction par lots atomiques, qui contient les opérations de stockage distincts too100 (limite de taille totale de 4 Mo). En supposant que hello même nombre de toobe entités récupérée, vous pouvez également interroger les données dans une même partition plus efficacement que les données qui s’étend sur les partitions (bien que lecture pour les recommandations sur l’interrogation des données de table).
* Limite d’extensibilité : tooentities d’accès stockées dans une partition unique ne peut pas être équilibrée, car les partitions prennent en charge les transactions atomiques par lots. Pour cette raison, la cible d’évolutivité hello pour une partition de table individuelle est inférieur à celui service de table hello dans sa globalité.  

En raison de ces caractéristiques des tables et des partitions, vous devez adopter hello suivant les principes de conception :  

* Les données que votre application cliente fréquemment mis à jour ou de l’interrogation Bonjour même unité logique de travail doit se trouver dans hello même partition.  Cela peut être, car votre application est l’agrégation des écritures ou vous souhaitez parti tootake des opérations atomiques par lots.  Ajoutons encore que les données d’une seule partition peuvent être interrogées plus efficacement dans une seule requête que les données de plusieurs partitions.
* Les données que votre application cliente ne pas insérer/mettre à jour ou une requête dans hello même unité logique de travail (requête unique ou mise à jour du lot) doit se trouver dans des partitions distinctes.  Une remarque importante n’est qu’aucun toohello limiter le nombre de clés de partition dans une table unique, afin d’avoir des millions de clés de partition n’est pas un problème et n’affectera pas les performances.  Par exemple, si votre application est un site de Web populaires avec la connexion de l’utilisateur, à l’aide de hello Id d’utilisateur en tant que clé de partition hello peut être un bon choix.  

#### <a name="hot-partitions"></a>Partitions actives
Une partition à chaud est une tâche qui reçoit un pourcentage disproportionné de compte de tooan hello du trafic, et ne peut pas être à charge équilibrée, car il s’agit d’une seule partition.  En règle générale, la création des partitions actives s’effectue de l’une des façons suivantes :  

##### <a name="subheading28"></a>Modèles « Ajouter après uniquement » et « Ajouter avant uniquement »
Hello « Ajouter uniquement » est un modèle dans lequel toutes les (ou quasiment tous) de hello trafic tooa donné PK augmentent et diminuent toohello conséquente heure actuelle.  Un exemple est si votre application a utilisé hello date actuelle en tant que clé de partition pour les données de journal.  Ainsi, toutes les insertions hello va toohello dernière partition dans la table, et système de hello ne peut pas équilibrer la charge, car toutes les écritures de hello sont toohello fin de votre table.  Si le volume de hello de partition toothat de trafic dépasse la cible d’évolutivité de niveau de la partition de hello, elle entraîne la limitation.  Il est mieux tooensure que le trafic est envoyé à des partitions toomultiple, hello de solde charge tooenable demande via votre table.  

##### <a name="subheading29"></a>Données à trafic élevé
Si vos résultats de schéma de partitionnement dans une seule partition qui comporte uniquement des données qui sert beaucoup plus que les autres partitions, vous pouvez également voir la limitation comme cible d’évolutivité hello pour une partition unique s’approche de cette partition.  Il s’agit d’une meilleure toomake sûr que vos résultats de schéma de partition dans aucun unique partitionnement approchant objectifs d’évolutivité hello.  

#### <a name="querying"></a>Interrogation
Cette section décrit des pratiques éprouvées pour interroger le service de table hello.  

##### <a name="subheading30"></a>Étendue de requête
Il existe plusieurs façons toospecify hello plage tooquery d’entités.  Hello Voici une présentation des utilisations hello de chaque.  

En règle générale, évitez d’analyses (requêtes supérieure à une seule entité), mais si vous devez analyser, essayez tooorganize vos données afin que vos analyses récupérer les données hello sans analyse ou le renvoi d’importantes quantités d’entités que vous n’avez pas besoin.  

###### <a name="point-queries"></a>Requêtes de point
Une requête de point récupère exactement une entité. Pour cela, en spécifiant la clé de partition hello et clé de ligne de hello entité tooretrieve. Ces requêtes s’avèrent particulièrement efficaces et il est conseillé de les utiliser autant que possible.  

###### <a name="partition-queries"></a>Requêtes de partition
Une requête de partition récupère un jeu de données qui partagent une clé de partition commune. En règle générale, les requêtes hello spécifie une plage de valeurs de clé de ligne ou une plage de valeurs de propriété d’entité dans la clé de partition tooa Ajout. Les requêtes de partition sont moins efficaces que les requêtes de point et doivent être utilisées avec modération.  

###### <a name="table-queries"></a>Requêtes de table
Une requête de table récupère un jeu d’entités ne partageant pas une clé de partition commune. Les requêtes de ce type ne sont pas efficaces et il est conseillé de les éviter dans la mesure du possible.  

##### <a name="subheading31"></a>Densité des requêtes
Un autre facteur clé pour l’efficacité des requêtes est un nombre hello d’entités retournées en tant que nombre toohello comparés d’entités toofind numérisés hello retournée défini. Si votre application effectue une requête de table avec un filtre pour une valeur de propriété qu’uniquement 1 % des partages de données hello, hello requête analyse 100 entités pour chaque une entité, qu'elle retourne. Hello objectifs d’évolutivité de table décrites précédemment nombre toohello d’entités analysées sont liés et pas hello nombre d’entités retournées : une densité basse de requête peut amener facilement hello table service toothrottle votre application, car il doit analyser autant entité de hello tooretrieve entités souhaité.  Consultez la section hello ci-dessous sur [dénormalisation](#subheading34) pour plus d’informations sur la façon de tooavoid cela.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Limitation hello quantité de données retournées
###### <a name="subheading32"></a>Filtrage
Lorsque vous savez qu’une requête retourne les entités que vous n’avez pas besoin dans l’application cliente de hello, envisagez d’utiliser une taille de hello filtre tooreduce Hello a retourné un ensemble. Alors que les entités hello ne retourné pas toohello client toujours comptabilisé dans les limites d’extensibilité hello, améliorent en raison de la taille de la charge réseau réduite de hello et hello réduit le nombre d’entités que votre application cliente doit traiter les performances de votre application .  Voir ci-dessus Remarque sur [densité de la requête](#subheading31), cependant – objectifs d’évolutivité hello concernent les nombre toohello d’entités analysées, une requête qui filtre les nombreuses entités peut toujours aboutira à la limitation, même si quelques entités sont retournées.  

###### <a name="subheading33"></a>Projection
Si votre application cliente doit uniquement un ensemble limité de propriétés à partir des entités hello dans votre table, vous pouvez utiliser la taille de hello toolimit projection de hello a retourné un ensemble de données. Comme avec le filtrage, cela permet de tooreduce de la charge réseau et le traitement client.  

##### <a name="subheading34"></a>Dénormalisation
Contrairement à l’utilisation de bases de données relationnelles, hello pratiques permettant d’interroger efficacement les données de la table entraîner toodenormalizing vos données. Autrement dit, la duplication hello mêmes données dans plusieurs entités (une pour chaque clé, vous pouvez utiliser les données de salutation toofind) nombre de hello toominimize d’entités qu’une requête doit analyser les besoins du client toofind hello données hello, au lieu d’utiliser tooscan grand nombre d’entités toofind les données de salutation votre application a besoin.  Par exemple, dans un site Web de commerce électronique, vous souhaiterez peut-être toofind une commande par ID de client hello (donner les commandes de ce client) et par date de hello (me donner les commandes à une date).  Dans le stockage de Table, il est meilleure entité de hello toostore (ou un tooit de référence) à deux reprises : une fois avec le nom de la Table, PK et Kit de ressources recherche toofacilitate par ID de client, une fois les toofacilitate recherchant par date de hello.  

#### <a name="insertupdatedelete"></a>Insertion/Mise à jour/Suppression
Cette section décrit des pratiques éprouvées pour la modification des entités stockées dans le service de table hello.  

##### <a name="subheading35"></a>Traitement par lot
Transactions par lots sont connues en tant qu’entité groupe de Transactions (ETG) dans le stockage Azure ; toutes les opérations de hello dans un ETG doivent être sur une partition unique dans une table unique. Si possible, utilisez ETGs tooperform insertions, mises à jour et suppressions en lots. Cela réduit le nombre de hello d’allers-retours à partir de votre serveur toohello d’application client, réduit hello nombre de transactions facturables (un ETG compte comme une transaction unique à des fins de facturation et peut contenir des opérations de stockage too100) et permet atomique mises à jour (toutes les opérations réussissent ou l’ensemble d’échouer dans un ETG). L’utilisation des ETG peut apporter des avantages non négligeables dans les environnements où les temps de latence sont élevés, tels que les appareils mobiles.  

##### <a name="subheading36"></a>Opération Upsert
Lorsque cela s'avère possible, il est conseillé d'utiliser des opérations de table **Upsert** . Il existe deux types d’opération **Upsert** ; tous deux peuvent se révéler plus efficaces que les opérations **Insert** et **Update** classiques :  

* **InsertOrMerge**: utilisez cette option lorsque vous souhaitez tooupload un sous-ensemble de propriétés de l’entité hello, mais ne savez pas si les entités hello existant déjà. Si l’entité hello existe, cet appel met à jour les propriétés de hello incluses dans hello **Upsert** opération et conserve toutes les propriétés existantes lorsqu’ils sont, si hello entité n’existe pas, il insère la nouvelle entité de hello. Il s’agit de projection de toousing similaire dans une requête, vous devez uniquement les propriétés de hello tooupload qui sont en cours de modification.
* **InsertOrReplace**: utilisez cette option lorsque vous souhaitez tooupload une toute nouvelle entité, mais vous ne savez pas si elle existe déjà. Vous n’utilisez cette option lorsque vous savez que hello téléchargé nouvellement entité est entièrement correct, car elle remplace complètement l’ancienne entité de hello. Par exemple, vous souhaitez entité hello tooupdate qui stocke l’emplacement actuel de l’utilisateur, quelle que soit ou non application hello a précédemment stocké des données d’emplacement pour l’utilisateur de hello ; nouvelle entité d’emplacement Hello est terminée, et vous n’avez pas besoin de toutes les informations de toute entité précédente.

##### <a name="subheading37"></a>Stockage de séries de données dans une seule entité
Parfois, une application stocke une série de données fréquemment doit avoir tooretrieve tous en même temps : par exemple, une application peut suivre l’utilisation du processeur au fil du temps dans l’ordre tooplot un graphique propagée de données de hello de hello des dernières 24 heures. Une approche consiste à entité d’une table de toohave par heure, avec chaque entité représentant une heure spécifique et le stockage de l’utilisation du processeur hello pour cette heure. tooplot ces données, l’application hello doivent les entités de hello tooretrieve contenant les données hello hello les dernières 24 heures.  

Vous pouvez également votre application peut stocker d’utilisation de hello du processeur pour chaque heure sous la forme d’une propriété distincte d’une entité unique : tooupdate chaque heure, votre application peut utiliser un seul **InsertOrMerge Upsert** appeler la valeur de hello tooupdate pour hello heure la plus récente. les données de salutation tooplot, application hello doit uniquement tooretrieve une seule entité au lieu de 24, pour une requête très efficace (voir ci-dessus la discussion sur [étendue de requête](#subheading30)).

##### <a name="subheading38"></a>Stockage de données structurées dans des objets blob
Les données structurées donnent parfois l’impression qu’elles devraient être placées dans les tables. Cependant, les plages d’entités sont toujours récupérées ensemble et peuvent être insérées par lots.  À cet égard, un fichier journal constitue un parfait exemple.  Dans ce cas, vous pouvez regrouper plusieurs minutes de journalisation et les insérer. Vous récupérez alors plusieurs minutes de journalisation à la fois.  Dans ce cas, pour des performances, il est mieux BLOB toouse plutôt que des tables, étant donné que vous pouvez réduire considérablement le nombre hello des objets écrits/retournés, ainsi généralement hello nombre de demandes qui doivent être effectuées.  

## <a name="queues"></a>Files d’attente
Dans toohello plus pratiques pour éprouvées [tous les Services](#allservices) décrit précédemment, suivant hello pratiques éprouvées s’appliquent en particulier le service de file d’attente toohello.  

### <a name="subheading39"></a>Limites d’extensibilité
Une seule file d’attente peut traiter environ 2 000 messages (1 Ko chacun) par seconde (chaque AddMessage, GetMessage et DeleteMessage compte pour un message). Si cela est insuffisant pour votre application, utilisez plusieurs files d’attente et répartir les messages de type hello entre eux.  

consultez les objectifs d’extensibilité actuels dans [Objectifs de performance et d’extensibilité d’Azure Storage](storage-scalability-targets.md).  

### <a name="subheading40"></a>Désactivation de Nagle
Consultez la section de hello sur la configuration de la table qui décrit l’algorithme Nagle de hello : algorithme Nagle de hello est généralement incorrect pour les performances hello de demandes de file d’attente, et vous devez les désactiver.  

### <a name="subheading41"></a>Taille des messages
Les performances et l’extensibilité des files d’attente diminuent quand la taille de message augmente. Vous devez placer seul hello informations hello récepteur doit être dans un message.  

### <a name="subheading42"></a>Récupération par lots
Vous pouvez récupérer les messages too32 à partir d’une file d’attente en une seule opération. Cela peut réduire le nombre de hello d’allers-retours à partir de l’application cliente hello, qui est particulièrement utile pour les environnements, tels que des appareils mobiles, avec une latence élevée.  

### <a name="subheading43"></a>Intervalle d'interrogation de file d'attente
La plupart des applications vérifier les messages à partir d’une file d’attente, ce qui peut être une des sources de plus grande hello de transactions pour cette application. Sélectionnez votre intervalle d’interrogation avec soin : interrogation trop fréquente, tooapproach de votre application peut entraîner des objectifs d’évolutivité hello pour la file d’attente hello. Toutefois, les transactions 200 000 pour 0,01 $ (au moment de hello de l’écriture), un seul processeur, l’interrogation d’une fois par seconde pour un mois reviendrait à moins de 15 cents coûts n’est pas généralement un facteur qui affecte le choix de l’intervalle d’interrogation.  

Pour plus d’informations relatives au coût, consultez [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
Vous pouvez utiliser **UpdateMessage** tooincrease hello invisibilité délai d’attente tooupdate informations d’état ou d’un message. Bien que cela soit puissant, n’oubliez pas que chaque **UpdateMessage** opération compte vers la cible d’évolutivité hello. Toutefois, cela peut être beaucoup plus efficace que d’avoir un flux de travail passe ensuite, un travail à partir d’une file d’attente toohello que chaque étape du travail de hello est terminée. À l’aide de hello **UpdateMessage** opération permet à votre message d’application toosave hello travail état toohello et ensuite continuer à travailler, au lieu de message de type hello ré-files d’attente pour l’étape suivante de hello du travail hello chaque fois qu’une étape est terminée.  

Pour plus d’informations, voir l’article hello [Comment : modifier le contenu de hello d’un message en file d’attente](../queues/storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Architecture de l’application
Vous devez utiliser les files d’attente toomake évolutive de l’architecture de votre application. suivant de Hello répertorie quelques méthodes que vous pouvez utiliser les files d’attente toomake votre application plus évolutive :  

* Vous pouvez utiliser les backlogs de toocreate de files d’attente de travail pour le traitement et lisser les charges de travail dans votre application. Par exemple, vous a une file d’attente les demandes de travail nécessitant de processeur tooperform utilisateurs telles que le redimensionnement des images téléchargées.
* Vous pouvez utiliser des parties de toodecouple les files d’attente de votre application afin que vous pouvez mettre à l’échelle indépendamment. Un serveur web frontal peut, par exemple, placer les résultats d’une enquête en file d’attente en vue de les stocker et de les analyser ultérieurement. Vous pouvez ajouter que plus tooprocess d’instances de rôle de travail hello des données de la file d’attente en fonction des besoins.  

## <a name="conclusion"></a>Conclusion
Cet article parlé de quelques hello courant, pratiques pour optimiser les performances lors de l’utilisation du stockage Azure éprouvées. Nous encourageons chaque tooassess de développeur d’application leur application auprès de chacun des hello ci-dessus pratiques et que vous envisagez agissant sur les performances exceptionnelles tooget recommandations hello pour leurs applications qui utilisent le stockage Azure.
