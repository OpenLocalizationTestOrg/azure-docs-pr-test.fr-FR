---
title: "sécurité de série aaaStorSimple 8000 | Documents Microsoft"
description: "Décrit la sécurité de hello et de fonctionnalités de confidentialité qui protègent votre service StorSimple, les appareils et les données localement et dans le cloud de hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 48dd449d2908c21fe05d0ed37a4dc6f3e306e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>Sécurité et protection des données StorSimple

## <a name="overview"></a>Vue d'ensemble

La sécurité est une préoccupation majeure pour toute personne qui adoptent une nouvelle technologie, surtout lorsque hello est utilisée avec des données confidentielles ou propriétaires. Lorsque vous évaluez différentes technologies, vous devez tenir compte des risques et des coûts relatifs à la protection des données. Microsoft Azure StorSimple fournit à la fois une solution de sécurité et confidentialité pour la protection des données, aidant tooensure :

* **La confidentialité** : seules les entités autorisées peuvent consulter vos données.
* **L’intégrité** : seules les entités autorisées peuvent modifier ou supprimer vos données.

Hello solution Microsoft Azure StorSimple se compose de quatre principaux composants qui interagissent entre eux :

* **Service de gestionnaire de périphériques StorSimple hébergé dans Microsoft Azure** – hello service Gestion des services que vous utilisez tooconfigure et approvisionner hello appareil StorSimple.
* **L’appareil StorSimple** : appareil physique installé dans votre centre de données. Tous les hôtes et les clients qui génèrent des données de l’appareil StorSimple toohello se connectent et les appareils hello gèrent les données de salutation et déplace toohello cloud Azure selon le cas.
* **Clients/hôtes connectés toohello périphérique** : hello dans votre infrastructure, les clients qui se connectent à l’appareil StorSimple toohello et générer des données doit toobe protégé.
* **Stockage cloud** – hello emplacement Bonjour Azure cloud où les données sont stockées.

Hello sections suivantes décrivent les fonctionnalités de sécurité de StorSimple de hello qui chacun de ces composants et les données hello qu’ils protègent. Il inclut également une liste de questions que vous aurez peut-être sur la sécurité de Microsoft Azure StorSimple et les réponses correspondantes hello.

## <a name="storsimple-device-manager-service-protection"></a>Protection du service StorSimple Device Manager

Hello service du Gestionnaire de périphériques StorSimple est un service de gestion hébergé dans Microsoft Azure, de toomanage tous les appareils StorSimple de votre organisation. Vous pouvez accéder hello service du Gestionnaire de périphériques StorSimple à l’aide de vos informations d’identification d’organisation de toolog sur toohello portail Azure via un navigateur web.

Accès toohello le Gestionnaire de périphériques StorSimple service nécessite que votre organisation a souscrit un abonnement Azure qui inclut StorSimple. Votre abonnement régit les fonctions hello auxquelles vous pouvez accéder dans hello portail Azure. Si votre organisation ne dispose pas d’un abonnement Azure et que vous souhaitez toolearn plus à leur sujet, consultez [Inscrivez-vous à Azure en tant qu’organisation](../active-directory/sign-up-organization.md).

Étant donné que hello StorSimple Device Manager service est hébergé dans Azure, il est protégé par les fonctionnalités de sécurité Azure hello. Pour plus d’informations sur les fonctionnalités de sécurité hello fournies par Microsoft Azure, accédez à toohello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

## <a name="storsimple-device-protection"></a>Protection de l’appareil StorSimple

l’appareil StorSimple Hello est un périphérique de stockage hybride local qui contient des lecteurs de solid state Drive (SSD) et les lecteurs de disque dur (HDD), ainsi que des contrôleurs redondants et des fonctionnalités de basculement automatique. les contrôleurs de Hello gèrent la hiérarchisation du stockage plaçant actuellement utilisées (ou à chaud) des données sur le stockage local (dans hello appareil StorSimple ou sur des serveurs locaux), lors du déplacement des données moins souvent utilisées dans le cloud toohello.

Seules les StorSimple toojoin hello service Gestionnaire de périphériques StorSimple que vous avez créé dans votre abonnement Azure les appareils sont autorisés. tooauthorize un appareil, vous devez l’inscrire avec hello service du Gestionnaire de périphériques StorSimple en fournissant la clé d’inscription hello. clé d’inscription Hello est une clé aléatoire de 128 bits générée dans hello portail Azure.

![Clé d'inscription du service](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn comment obtenir un go de clé, service d’inscription trop[étape 2 : clé d’inscription Get hello](storsimple-8000-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).

clé d’inscription Hello est une longue clé qui contient plus de 100 caractères. Vous pouvez copier la clé de hello et enregistrez-le dans un fichier texte dans un emplacement sécurisé afin que vous pouvez l’utiliser tooauthorize des périphériques supplémentaires si nécessaire. Si la clé d’inscription hello est perdue après avoir inscrit votre premier appareil, vous pouvez générer une nouvelle clé à partir de hello service du Gestionnaire de périphériques StorSimple. Cela n’affectera pas opération hello des périphériques existants.

Après l’inscription d’un appareil, il utilise des jetons toocommunicate avec Microsoft Azure. clé d’inscription Hello n’est pas utilisé après l’inscription de périphérique.

> [!NOTE]
> Nous vous recommandons de régénérer la clé d’inscription hello après chaque utilisation.


## <a name="protect-your-storsimple-solution-via-passwords"></a>Protection de votre solution StorSimple par des mots de passe

Les mots de passe sont un aspect important de la sécurité de l’ordinateur et sont largement utilisés dans la solution de StorSimple hello toohelp vous assurer que vos données sont uniquement des utilisateurs tooauthorized accessible. StorSimple vous permet de hello tooconfigure suivant les mots de passe :

* Mot de passe Administrateur d’appareil StorSimple
* Mots de passe initiateur et cible de protocole CHAP (Challenge Handshake Authentication Protocol)
* Mot de passe de gestionnaire d’instantanés StorSimple

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Windows PowerShell pour StorSimple et hello mot de passe administrateur de périphérique StorSimple

Windows PowerShell pour StorSimple est une interface de ligne de commande que vous pouvez utiliser l’appareil StorSimple toomanage hello. Windows PowerShell pour StorSimple a des fonctionnalités qui vous permettent de tooregister votre appareil, configurez hello interface réseau sur votre appareil, installer certains types de mises à jour, résoudre les problèmes de votre appareil en accédant à la session de support hello et modifier l’état de l’appareil hello . Vous pouvez accéder à Windows PowerShell pour StorSimple par connexion console série toohello sur l’appareil de hello ou à l’aide de la communication à distance de Windows PowerShell.

L’accès distant PowerShell peut être effectué via HTTPS ou HTTP. Si la gestion à distance via HTTPS est activée, vous devez la gestion à distance toodownload hello de certificat à partir de l’appareil de hello et l’installer sur les clients distants hello. Pour plus d’informations sur la communication à distance PowerShell, consultez trop[se connecter à distance de l’appareil StorSimple tooyour](storsimple-8000-remote-connect.md).

Une fois que vous utilisez Windows PowerShell pour StorSimple tooconnect toohello appareil, vous devez toolog de mot de passe tooprovide hello appareil administrateur sur l’appareil de toohello.

![Mot de passe d'administrateur de l'appareil](./media/storsimple-security/DeviceAdminPW.png)

Gardez hello suivant les meilleures pratiques à l’esprit :

* La gestion à distance est désactivée par défaut. Vous pouvez utiliser tooenable de service de gestionnaire de périphériques StorSimple hello il. Comme meilleure pratique de sécurité, l’accès à distance doivent être activé uniquement pendant la période pendant laquelle il est réellement nécessaire de hello.
* Si vous modifiez le mot de passe hello, être toonotify que tous les utilisateurs de l’accès à distance afin qu’ils ne soient pas confrontés une perte de connectivité inattendus.
* Hello service du Gestionnaire de périphériques StorSimple ne peut pas récupérer les mots de passe existants : il peut uniquement les réinitialiser. Nous vous recommandons de stocker tous les mots de passe dans un emplacement sécurisé afin que vous n’avez pas tooreset un mot de passe si elle est oublié. Si vous n’avez pas besoin tooreset un mot de passe, être toonotify que tous les utilisateurs avant que vous le réinitialiser.

Vous pouvez accéder interface Windows PowerShell de hello en utilisant un appareil de toohello connexion série. Vous pouvez également y accéder à distance à l’aide de HTTP ou HTTPS, qui offre une sécurité supplémentaire. Le protocole HTTPS assure un niveau de sécurité supérieur à une connexion série ou HTTP. Toutefois, toouse HTTPS, vous devez d’abord installer un certificat sur ordinateur hello client qui accédera l’appareil de hello. Vous pouvez télécharger le certificat d’accès à distance hello à partir de la page de configuration de périphérique hello Bonjour service du Gestionnaire de périphériques StorSimple. En cas de perte de certificat hello pour l’accès à distance, vous devez télécharger un nouveau certificat et propagez-le tooall les clients qui sont autorisés toouse la gestion à distance.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Mots de passe initiateur et cible de protocole CHAP (Challenge Handshake Authentication Protocol)

Le protocole CHAP est un schéma d’authentification utilisé par hello identité de hello toovalidate l’appareil StorSimple de clients distants. vérification de Hello est basée sur un mot de passe. Le protocole CHAP peut être à sens unique (unidirectionnel) ou mutuel (bidirectionnel). Authentification CHAP unidirectionnelle, cible de hello (appareil de StorSimple hello) authentifie un initiateur (hôte). CHAP mutuelle ou inverse requiert la cible de hello authentifier l’initiateur de hello et puis hello initiateur doit authentifier hello cible. Votre StorSimple peut être configuré toouse que soit la méthode.

Tenez compte des éléments suivants de hello lorsque vous configurez le protocole CHAP :

* nom d’utilisateur CHAP Hello doit contenir 233 caractères maximum.
* mot de passe CHAP Hello doit comprendre entre 12 et 16 caractères. Toute tentative toouse un nom d’utilisateur ou le mot de passe plus long entraîne un échec d’authentification sur l’ordinateur hôte de Windows hello.
* Vous ne pouvez pas utiliser hello même mot de passe pour hello CHAP initiateur et cible CHAP de hello.
* Après avoir défini un mot de passe hello, il peut être modifié, mais il ne peut pas être récupéré. Si le mot de passe hello est modifié, être toonotify que tous les utilisateurs de l’accès à distance afin de pouvoir connecter avec succès l’appareil StorSimple toohello.

Pour plus d’informations sur le protocole CHAP et comment tooconfigure pour votre solution StorSimple, accédez trop[configurer CHAP pour votre appareil StorSimple](storsimple-8000-configure-chap.md).

### <a name="storsimple-snapshot-manager-password"></a>Mot de passe de gestionnaire d’instantanés StorSimple

Gestionnaire d’instantanés StorSimple est un composant logiciel enfichable Microsoft Management Console (MMC) qui utilise des groupes de volumes et sauvegardes cohérentes avec les applications de hello Windows Volume Shadow Copy Service toogenerate. En outre, vous pouvez utiliser les clone et Gestionnaire d’instantanés StorSimple toocreate les planifications de sauvegarde ou restaurer des volumes.

Lorsque vous configurez un gestionnaire d’instantanés StorSimple de toouse appareil, vous serez mot de passe requis tooprovide hello Gestionnaire d’instantanés StorSimple. Ce mot de passe est d'abord défini dans Windows PowerShell pour StorSimple lors de l'inscription. mot de passe Hello peut également être défini et a été remplacée par hello service du Gestionnaire de périphériques StorSimple. Ce mot de passe authentifie l’appareil hello avec Gestionnaire d’instantanés StorSimple.

![Mot de passe de gestionnaire d’instantanés StorSimple](./media/storsimple-security/SnapshotMgrPassword.png)

mot de passe de gestionnaire d’instantanés StorSimple Hello doit comporter 14 too15 caractères et doit contenir au moins 3 d’une combinaison de caractères en majuscules, minuscules, numériques et spéciaux. Après avoir défini un mot de passe du Gestionnaire d’instantanés StorSimple hello, il peut être modifié, mais il ne peut pas être récupéré. Si vous modifiez le mot de passe hello, être toonotify que tous les utilisateurs distants.

Pour plus d’informations sur StorSimple Snapshot Manager, accédez trop[Nouveautés du Gestionnaire d’instantanés StorSimple ?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>Meilleures pratiques relatives aux mots de passe

Nous vous recommandons d’utiliser suivant de hello instructions toohelp Assurez-vous que les mots de passe StorSimple sont forts et la protection :

* Modifiez votre mot de passe tous les trois mois. La modification des mots de passe hello est appliquée par an.
* Utilisez des mots de passe forts. Pour plus d’informations, consultez trop[créer des mots de passe plus forts et de les protéger](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/).
* Utilisez toujours des mots de passe différents pour différents mécanismes d’accès ; chacun des mots de passe hello que vous spécifiez doit être unique.
* Ne partagent pas les mots de passe avec les personnes qui n’est pas autorisé tooaccess hello StorSimple.
* Ne pas allusion à un mot de passe devant d’autres personnes ou indicateur de format hello de mot de passe.
* Si vous pensez qu’un compte ou un mot de passe a été compromise, le service de sécurité hello tooyour incident de rapports.
* Traitez tous les mots de passe comme des informations sensibles et confidentielles. 

## <a name="storsimple-data-protection"></a>Protection des données StorSimple

Cette section décrit les fonctionnalités de sécurité StorSimple hello protéger les données stockées et les données en transit.

Comme décrit dans d’autres sections, les mots de passe sont utilisé tooauthorize et authentifient les utilisateurs avant qu’ils peuvent avoir accès tooyour StorSimple solution. La protection des données contre les utilisateurs non autorisés pendant leur transfert entre les systèmes de stockage et pendant leur stockage est également primordiale. Hello sections suivantes décrivent les fonctionnalités de protection des données hello fournies avec StorSimple.

> [!NOTE]
> La déduplication offre une protection supplémentaire pour les données stockées sur l’appareil StorSimple hello et dans le stockage Microsoft Azure. Lorsque les données dédupliquées, objets de données hello sont stockés séparément des toomap de métadonnées utilisées hello et y accéder : aucune donnée de contexte au niveau du stockage disponible tooreconstruct hello en fonction de la structure d’un volume, système de fichiers ou nom de fichier.


## <a name="protect-data-flowing-through-hello-service"></a>Protéger les données transitant par le service de hello

Hello principal objectif de hello service du Gestionnaire de périphériques StorSimple est toomanage et configurer l’appareil StorSimple hello. Hello, le Gestionnaire de périphériques StorSimple service s’exécute dans Microsoft Azure. Vous utilisez hello données de configuration de périphérique tooenter portail Azure, Microsoft Azure utilise ensuite hello le Gestionnaire de périphériques StorSimple service toosend hello toohello l’unité de données. Utilise StorSimple un système de paires de clés asymétriques toohelp vous assurer que la compromission de hello service Azure ne provoque pas compromettre stockées des informations.

![Chiffrement des données à la volée](./media/storsimple-security/DataEncryption.png)

système de clés asymétriques Hello contribue à protéger les données de hello qui transitent via le service de hello comme suit :

1. Un certificat de chiffrement de données qui utilise une paire de clés publique et privée asymétriques est généré sur l’appareil de hello et est utilisé tooprotect hello données. les clés de Hello sont générées lorsque le premier périphérique de hello est inscrit.
2. clés de certificat de chiffrement de données Hello sont exportés dans un fichier d’échange d’informations personnelles (.pfx) qui est protégé par hello clé de chiffrement, qui est une clé forte de 128 bits générée de façon aléatoire par le premier périphérique de hello lors de l’inscription.
3. en toute sécurité la clé publique de Hello du certificat de hello est rendue disponible toohello service du Gestionnaire de périphériques StorSimple et clé privée de hello est conservée avec le périphérique de hello.
4. Service de hello saisie est chiffré à l’aide de données hello clé publique et déchiffrées à l’aide de la clé privée de hello stockée sur l’appareil de hello, garantissant que le service Azure hello ne peut pas déchiffrer les données de hello circuler toohello appareil.

clé de chiffrement de données de service Hello est généré uniquement sur hello premier appareil inscrit avec le service de hello. Tous les autres appareils qui sont inscrits avec le service de hello doivent utiliser hello même clé de chiffrement de données de service.

> [!IMPORTANT]
> Il est très important toomake une copie de la clé de chiffrement de données de service hello et enregistrez-le dans un emplacement sécurisé. Une copie de la clé de chiffrement de données de service hello doit être stockée de sorte qu’il est accessible à toute personne autorisée et peut être communiquée facilement toohello administrateur de l’appareil.
> 
> Si la clé de chiffrement de données de service hello est perdue, une personne du support technique Microsoft peut vous aider à tooretrieve il fourni que vous avez au moins un périphérique dans un état en ligne. Nous vous recommandons de changer de clé de chiffrement de données de service hello après que qu’il est récupéré. Pour obtenir des instructions, consultez trop[clé de chiffrement de données modifiées hello service](storsimple-service-dashboard.md#change-the-service-data-encryption-key).

Vous pouvez modifier la clé de chiffrement de données de service hello et certificat de chiffrement de données correspondante hello en sélectionnant hello **modification de clé de chiffrement** option sur le tableau de bord de service hello. tooensure que la sécurité des données n’est pas compromise, vous devez utiliser une physique StorSimple périphérique toochange hello clé de chiffrement. Modification des clés de chiffrement hello requiert que tous les appareils être mis à jour avec la nouvelle clé de hello. Par conséquent, nous vous recommandons de changer de clé de hello lorsque tous les appareils sont en ligne. Si des appareils sont hors connexion, leurs clés peuvent être modifiées plus tard. appareils Hello avec des clés obsolètes seront en mesure de toorun sauvegardes, mais ils ne sera pas en mesure de toorestore données jusqu'à ce que la clé de hello est mise à jour. Pour plus d’informations, consultez trop[tableau de bord utilisation hello le Gestionnaire de périphériques StorSimple service](storsimple-8000-service-dashboard.md).

clé de chiffrement de données de service Hello et certificat de chiffrement de données hello n’expirent pas. Toutefois, nous vous recommandons de modifier le chiffrement de données de service hello clé annuellement toohelp empêcher la compromission de la clé.

## <a name="protect-data-at-rest"></a>Protection des données au repos

l’appareil StorSimple Hello gère les données en les stockant dans les niveaux localement et dans le cloud hello, selon la fréquence d’utilisation. Tous les hôtes d’ordinateurs qui sont connectés toohello envoi données toohello un périphérique, qui déplace ensuite les données dans le cloud toohello, selon le cas. Données transférées à partir de hello appareil toohello cloud en toute sécurité sur Internet de hello. Chaque périphérique possède une cible iSCSI qui couvre tous les volumes partagés sur cet appareil. Toutes les données sont chiffrées avant d’être envoyée toocloud stockage. 

![Clé de chiffrement de stockage cloud](./media/storsimple-security/CloudStorageEncryption.png)

toohelp garantir la sécurité de hello et l’intégrité des données déplacées toohello cloud, StorSimple vous permet de clés de chiffrement de stockage cloud toodefine comme suit :

* Vous spécifiez la clé de chiffrement de stockage cloud hello lorsque vous créez un conteneur de volume. clé de Hello ne peut pas être modifiée ou ajoutée plus tard.
* Tous les volumes dans un partage de conteneur de volume hello la même clé de chiffrement. Si vous souhaitez une autre forme de chiffrement pour un volume spécifique, nous vous recommandons de créer un nouveau toohost de conteneur de volume ce volume.
* Lorsque vous entrez la clé de chiffrement de stockage cloud hello Bonjour service du Gestionnaire de périphériques StorSimple, clé de hello est chiffrée à l’aide de la partie publique de hello de clé de chiffrement de données de service hello, puis envoyées toohello appareil.
* clé de chiffrement de stockage cloud Hello n’est pas stocké dans le service hello et est connue uniquement toohello appareil.
* La spécification d’une clé de chiffrement de stockage cloud est facultative. Vous pouvez envoyer des données qui ont été chiffrées au périphérique de toohello hello hôte.

### <a name="additional-security-best-practices"></a>Meilleures pratiques supplémentaires en matière de sécurité

* Fractionner le trafic : isolez votre SAN iSCSI du trafic utilisateur sur un réseau LAN d'entreprise en déployant un réseau totalement séparé et en utilisant des réseaux locaux virtuels où l'isolation physique n'est pas une option. Un réseau dédié pour le stockage iSCSI garantira la sécurité de hello et des performances de vos données critiques. Le fait de mélanger le stockage et le trafic utilisateur sur un réseau LAN d'entreprise n'est pas recommandé et peut augmenter la latence, ainsi que provoquer des défaillances du réseau.
* Pour une sécurité réseau côté hôte, utilisez des interfaces réseau qui prennent en charge le moteur de déchargement TCP/IP (TOE). TOE réduit la charge de l’UC par le traitement TCP sur la carte réseau de hello.

## <a name="protect-data-via-storage-accounts"></a>Protection des données par les comptes de stockage

Chaque abonnement Microsoft Azure peut créer un ou plusieurs comptes de stockage. (Un compte de stockage fournit un espace de noms unique pour l’utilisation des données stockées dans hello Azure cloud). Compte de stockage tooa accès est contrôlé par clés hello abonnement et d’accès associés à ce compte de stockage.

Lorsque vous créez un compte de stockage, Microsoft Azure génère deux clés d’accès de stockage de 512 bits, qui est utilisé pour l’authentification lors de l’appareil StorSimple hello accède au compte de stockage hello. Notez que seule une des clés est utilisée. Hello autre clé est gardée en réserve, ce qui permet des clés hello toorotate régulièrement. toorotate clés, que vous apportez hello secondaire clé active et ensuite supprimer hello clé primaire. Vous pouvez ensuite créer une nouvelle clé à utiliser lors de la rotation suivante de hello. (De nombreux centres de données ont recours à la rotation des clés pour des raisons de sécurité).

Nous vous recommandons de suivre ces méthodes recommandées pour la rotation des clés :

* Vous devez faire pivoter clés compte de stockage régulièrement toohelp vous assurer que votre compte de stockage n’est pas accessible par les utilisateurs non autorisés.
* Périodiquement, votre administrateur Azure doit changer ou régénérer la clé primaire ou secondaire de hello à l’aide de section de stockage hello Hello compte de stockage Azure toodirectly portail accès hello.

## <a name="protect-data-via-encryption"></a>Protection des données par chiffrement

StorSimple utilise hello suivant tooprotect les données stockées dans les algorithmes de chiffrement ou de déplacement entre les composants hello de votre solution StorSimple.

| Algorithme | Longueur de clé | Protocoles/applications/commentaires |
| --- | --- | --- |
| RSA |2 048 |RSA PKCS 1 v1.5 est utilisé par hello tooencrypt portail Azure des données de configuration sont envoyées toohello périphérique : par exemple, stockage compte les informations d’identification, configuration de l’appareil StorSimple et les clés de chiffrement de stockage en nuage. |
| AES |256 |AES avec CBC est la partie publique de hello tooencrypt utilisés de la clé de chiffrement de données de service hello avant d’être envoyée à partir de l’appareil StorSimple hello toohello portail Azure. Il est également utilisé par les données tooencrypt périphérique StorSimple hello et avant l’envoi des données de hello toohello compte de stockage cloud. |

## <a name="storsimple-cloud-appliance-security"></a>Sécurité StorSimple Cloud Appliance

[!INCLUDE [storsimple Cloud Appliance security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>Forum Aux Questions (FAQ)

Hello Voici quelques questions et réponses sur la sécurité et de Microsoft Azure StorSimple.

**Q :** Mon service est compromis. Quelles doivent être mes étapes suivantes ?

**R :** vous devez immédiatement changer la clé de chiffrement de données de service hello et les clés de compte de stockage hello hello compte de stockage qui est utilisé pour stocker les données. Pour obtenir des instructions, consultez :

* [Modifier la clé de chiffrement de données de service hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Rotation des clés de comptes de stockage](storsimple-8000-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**Q :** vous disposez d’un nouveau périphérique StorSimple demandant clé d’inscription hello. Comment la récupérer ?

**R :** cette clé a été créée lors de la création de service du Gestionnaire de périphériques StorSimple hello. Lorsque vous utilisez un périphérique de hello le Gestionnaire de périphériques StorSimple service tooconnect toohello, vous pouvez utiliser tooview de page de démarrage rapide de service hello ou clé d’inscription hello régénérer. Création d’un service d’inscription n’affectera pas les appareils inscrits existants hello. Pour obtenir des instructions, consultez :

* [Afficher ou régénérer la clé d’inscription hello](storsimple-8000-manage-service.md##regenerate-the-service-registration-key)

**Q :** J’ai perdu ma clé de chiffrement des données du service. Que faire ?

**R :** Contactez le support technique Microsoft. Se connecter tooa session de support sur votre appareil et de vous aider à récupérer la clé de hello (fournie au moins une unité est en ligne). Immédiatement après avoir obtenu la clé de chiffrement de données de service hello, vous ne devez modifier tooensure cette nouvelle clé de hello est connue uniquement tooyou. Pour obtenir des instructions, consultez :

* [Modifier la clé de chiffrement de données de service hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**Q :** j’ai autorisé un périphérique pour le changement de clé de chiffrement de données service, mais n’a pas démarré le processus de modification de la clé hello. Que dois-je faire ?

**R :** si l’expiration du délai hello, avoir besoin de périphérique de hello tooreauthorize pour modification clé de chiffrement de données de service de hello et recommencez le processus de hello.

**Q :** j’ai modifié la clé de chiffrement de données de service hello, mais je n’a pas pu tooupdate hello autres appareils dans les 4 heures. Ont toostart à nouveau ?

**R :** hello période de 4 heures concerne seulement origine hello modification. Une fois que vous démarrez le processus de mise à jour hello sur hello autorisé l’appareil StorSimple, l’autorisation hello est valide jusqu'à ce que tous les appareils sont mis à jour.

**Q :** notre administrateur StorSimple a quitté l’entreprise de hello. Que dois-je faire ?

**R :** modifiez et réinitialisez les mots de passe qui autorise l’appareil StorSimple accès toohello et modifiez hello service données chiffrement clé tooensure que nouvelles informations de hello ne sont pas connues toounauthorized personnel de hello. Pour obtenir des instructions, consultez :

* [Utilisez hello le Gestionnaire de périphériques StorSimple service toochange vos mots de passe storsimple](storsimple-8000-change-passwords.md)
* [Modifier la clé de chiffrement de données de service hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Configuration de CHAP pour votre appareil StorSimple](storsimple-8000-configure-chap.md)

**Q :** je veux tooprovide hello Gestionnaire d’instantanés StorSimple mot de passe tooa hôte qui se connecte à l’appareil StorSimple toohello mais hello le mot de passe n’est pas disponible. Que puis-je faire ?

**R :** si vous avez oublié le mot de passe hello, vous devez créer un nouveau. Ensuite, veillez à tooinform tous les utilisateurs existants qui hello de mot de passe a été modifié et qu’ils doivent mettre à jour leur toouse clients hello nouveau mot de passe. Pour obtenir des instructions, consultez :

* [Modifier le mot de passe de gestionnaire d’instantanés StorSimple hello](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password)
* [Authentification d’un appareil](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**Q :** certificat hello pour toohello d’accès à distance de Windows PowerShell pour StorSimple a été modifié sur l’appareil de hello. Comment mettre à jour mes clients d’accès à distance ?

**R :** vous pouvez télécharger le certificat de nouveau hello de hello service du Gestionnaire de périphériques StorSimple et lui toobe installé dans le magasin de certificats hello de vos clients d’accès à distance. Pour obtenir des instructions, consultez :

* [Applet de commande Import-Certificate](https://technet.microsoft.com/library/hh848630.aspx)

**Q :** mes données sont-elles protégées si hello service du Gestionnaire de périphériques StorSimple est compromis ?

**R :** Les données de configuration du service sont toujours chiffrées avec votre clé publique lorsque vous les affichez dans un navigateur Web. Car le service de hello n’a pas clé privée d’accès toohello, service de hello à ne pas être en mesure de toosee toutes les données. Si hello service du Gestionnaire de périphériques StorSimple est compromis, aucun impact n’est, qu’il ne font a aucune clés stockées dans hello service du Gestionnaire de périphériques StorSimple.

**Q :** si quelqu'un obtient le certificat de chiffrement de données access toohello, seront mes données compromises ?

**R :** Microsoft Azure stocke la clé de chiffrement de données du client hello (fichier .pfx) dans un format chiffré. Comme fichier .pfx de hello est chiffré et hello service StorSimple n’a pas fichier .pfx de hello service données chiffrement toodecrypt clé hello, faire le fichier .pfx de toohello accès expose pas les clés secrètes.

**Q :** Que se passe-t-il si une entité gouvernementale demande mes données à Microsoft ?

**R :** , car toutes les données de hello sont chiffrées sur le service de hello et hello clé privée est gardée appareil de hello, hello gouvernemental entité doit demander au client hello pour les données de salutation.

## <a name="next-steps"></a>Étapes suivantes

[Déploiement de votre appareil StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

