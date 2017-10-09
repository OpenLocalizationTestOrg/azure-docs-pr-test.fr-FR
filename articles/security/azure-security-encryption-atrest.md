---
title: aaaMicrosoft Azure Data chiffrement au repos | Documents Microsoft
description: "Cet article fournit une vue d’ensemble du chiffrement des données de Microsoft Azure au repos, hello possibilités et considérations générales."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Chiffrement des données au repos d’Azure
Il existe plusieurs outils au sein des données de toosafeguard Microsoft Azure en fonction des besoins de sécurité et conformité tooyour de l’entreprise. Ce document se concentre sur comment est protégé au repos dans Microsoft Azure traite des différents composants qui participe à la mise en œuvre de protection de données hello hello et passe en revue les avantages et inconvénients des approches de protection de gestion de clés différentes hello. 

Le chiffrement au repos est une exigence de sécurité courante. Un avantage de Microsoft Azure est que les organisations peuvent permettre le chiffrement au repos sans avoir coût hello d’implémentation et de gestion et hello risque d’une solution de gestion de clés personnalisés. Les organisations ont option hello Azure permet de gérer complètement le chiffrement au repos. En outre, les organisations ont différentes options tooclosely gérer le chiffrement ou des clés de chiffrement.

## <a name="what-is-encryption-at-rest"></a>Qu’est-ce que le chiffrement au repos ?
Chiffrement au repos fait référence toohello chiffrement encodage (chiffrement) des données lorsqu’il est conservé. Hello chiffrement au niveau des conceptions de Rest dans Azure utilisez tooencrypt de chiffrement symétrique et déchiffrer les grandes quantités de données rapidement en fonction de modèle conceptuel simple de tooa :

- Une clé de chiffrement symétrique est utilisé tooencrypt données car elle est persistante 
- Hello la même clé de chiffrement est utilisé toodecrypt que les données qu’il est préparé pour une utilisation dans la mémoire
- Les données peuvent être partitionnées, et des clés différentes peuvent être utilisées pour chaque partition
- Clés doivent être stockées dans un emplacement sécurisé avec des stratégies de contrôle d’accès limitant l’accès toocertain identités et l’utilisation de la clé de journalisation. Les clés de chiffrement de données chiffrées souvent au moyen de limiter l’accès chiffrement asymétrique toofurther (présentés dans hello *clé hiérarchie*, plus loin dans cet article)

Hello ci-dessus décrit hello haut niveau des éléments en commun de chiffrement au repos. Dans la pratique, les scénarios de gestion et de contrôle des clés, ainsi que les garanties de scalabilité et de disponibilité, nécessitent des mécanismes supplémentaires. Les concepts et les composants du chiffrement des données au repos de Microsoft Azure sont décrits ci-dessous.

## <a name="hello-purpose-of-encryption-at-rest"></a>objectif Hello du chiffrement au repos
Chiffrement au repos est prévue tooprovide protection des données pour les données au repos (comme décrit ci-dessus). Les attaques contre les données au repos incluent matériel de toohello tentatives tooobtain accès physique sur le hello les données sont stockées et puis compromission hello contenait des données. Dans une telle attaque, lecteur de disque dur d’un serveur peut avoir été mauvaise pendant la maintenance de disque dur de hello tooremove permettre à un attaquant. Les intrus hello ultérieure place disque hello dans un ordinateur sous leurs données de contrôle tooattempt tooaccess hello. 

Chiffrement au repos est la personne malveillante de hello tooprevent conçu à partir de l’accès aux données de salutation non chiffrée en s’assurant que les données sont chiffrées sur le disque de hello. Si un attaquant tooobtain un disque dur avec de tels chiffré des données et aucune clé de chiffrement toohello accès, les intrus hello ne seraient pas compromettre les données hello sans difficulté. Dans ce scénario, un attaquant tooattempt les attaques contre les données chiffrées qui sont beaucoup plus complexes et consommatrices de ressources que l’accès à des données sur un disque dur non chiffrées. Pour cette raison, le chiffrement au repos est fortement recommandé et constitue une exigence de haute priorité pour de nombreuses organisations. 

Dans certains cas, le chiffrement au repos est nécessaire pour les besoins de l’organisation en matière de gouvernance et de conformité des données. Les réglementations publiques et de l’industrie, comme HIPAA, PCI et FedRAMP, et les exigences réglementaires internationales, définissent des protections spécifiques via des processus et des stratégies quant aux exigences de protection et de chiffrement des données. Pour la plupart de ces réglementations, le chiffrement au repos est une mesure obligatoire nécessaire à la conformité de la protection et de la gestion des données. 

En outre toocompliance et respect des obligations réglementaires, le chiffrement au repos doit être perçu comme une fonction de la plateforme de défense en profondeur. Tandis que Microsoft fournit une plateforme compatible pour les services, applications, données, une installation complète et la sécurité physique, données de contrôle d’accès et l’audit, il est important tooprovide « chevauchement » sécurité des mesures supplémentaires dans le cas de hello autres sécurité mesure échoue. Le chiffrement au repos fournit un mécanisme de défense supplémentaire de cet ordre.

Microsoft est chiffrement tooproviding validée au niveau des options de rest entre les services de cloud computing et tooprovide clients approprié la facilité de gestion de clés de chiffrement et toologs accès affichage lorsque les clés de chiffrement sont utilisées. En outre, Microsoft s’emploie objectif hello, consistant à toutes les données client sont chiffrées au repos par défaut.

## <a name="azure-encryption-at-rest-components"></a>Composants du chiffrement au repos d’Azure

Comme décrit précédemment, hello du chiffrement au repos vise que les données sont rendues persistantes sur disque sont chiffrées avec une clé secrète de chiffrement. tooachieve cet objectif sécuriser la création de la clé, de stockage, de contrôle d’accès et de gestion de chiffrement hello clés doivent être fournis. Bien que les détails varient, Azure services de chiffrement sur les implémentations de Rest peuvent être décrits en termes de hello ci-dessous les concepts illustrés puis Bonjour suivant schéma.

![Composants](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>coffre de clés Azure

emplacement de stockage de Hello des clés de chiffrement hello et les clés d’accès contrôle toothose est chiffrement tooan central au modèle rest. les clés de Hello doivent toobe hautement sécurisé, mais il est facile à gérer par les utilisateurs spécifiés et les services de toospecific disponibles. Pour les services Azure, Azure Key Vault est hello recommandé de solution de stockage de clés et offre une expérience de gestion courantes sur les services. Les clés sont stockés et gérés dans des coffres de clé et coffre de clés tooa accès peut être donné toousers ou services. Azure Key Vault prend en charge la création de clés par les clients ou l’importation de clés des clients pour les utiliser dans des scénarios où les clés de chiffrement sont gérées par ces clients.

### <a name="azure-active-directory"></a>Azure Active Directory

Clés de hello toouse autorisations stockées dans Azure Key Vault, toomanage ou tooaccess les pour le chiffrement au repos chiffrement et le déchiffrement, peut être donné tooAzure les comptes Active Directory. 

### <a name="key-hierarchy"></a>Hiérarchie des clés

Généralement, plusieurs clés de chiffrement sont utilisées dans une implémentation du chiffrement au repos. Chiffrement à clé asymétrique est utile pour établir l’approbation de hello et authentification nécessaire pour la gestion et d’accès de la clé. Un chiffrement symétrique est plus efficace pour le chiffrement et le déchiffrement en bloc, permettant un chiffrement plus fort et de meilleures performances. En outre, la limitation utiliser hello un diminue de clé de chiffrement unique risque de hello hello clé sera compromise et hello coût de rechiffrement lorsqu’une clé doit être remplacée. avantages de hello tooleverage de chiffrement symétrique et asymétrique et limite hello utilisation et l’exposition d’une clé unique, le chiffrement Azure sur les modèles rest utiliser une hiérarchie de clé de hello les types de clés suivants :

- **Clé de chiffrement de données (DEK)** – une clé symétrique de AES256 utilisé tooencrypt une partition ou un bloc de données.  Une même ressource peut avoir plusieurs partitions et de nombreuses clés de chiffrement des données. Le chiffrement de chaque bloc de données avec une clé différente rend les attaques d’analyse du chiffrement plus difficiles. Accès tooDEKs est requis par instance de fournisseur ou une application de ressource hello chiffrer et déchiffrer un bloc spécifique. Lorsqu’une clé DEK est remplacée par une nouvelle clé uniquement hello données dans son bloc associé doivent être chiffrées de nouveau avec la nouvelle clé de hello.
- **Clé de chiffrement de clé (KEK)** – une clé de chiffrement à clé asymétrique utilisée tooencrypt hello clés de chiffrement de données. Utilisation d’une clé de chiffrement de clé permet de hello des clés de chiffrement de données eux-mêmes toobe chiffré et contrôlée. entité Hello qui a accès toohello KEK peut être différent de celui entité hello nécessitant hello DEK. Cela permet un accès toohello DEK d’entité toobroker à des fins de hello d’assurer un accès limité de chaque partition de toospecific clé DEK. Hello veillent étant requis toodecrypt hello DEK, hello veillent est effectivement un point unique par lequel DEK peut être supprimés efficacement par la suppression de hello de clés.

Clés de chiffrement de données Hello, chiffrées avec hello clés de chiffrement de clé sont stockées séparément, et uniquement une entité avec toohello accès que clé de cryptage peut obtenir toutes les clés de chiffrement des données chiffrées avec cette clé. Différents modèles de stockage des clés sont pris en charge. Nous allons décrire chaque modèle plus en détail plus loin dans la section suivante de hello.

## <a name="data-encryption-models"></a>Modèles de chiffrement des données

Présentation des hello différents modèles de chiffrement et leurs avantages et inconvénients est essentiel pour comprendre comment hello que différents fournisseurs de ressources dans Azure implémenter le chiffrement au repos. Ces définitions sont partagées entre tous les fournisseurs de ressources de taxonomie et langage commun de tooensure Azure. 

Il existe trois scénarios de chiffrement côté serveur :

- Chiffrement côté serveur à l’aide de clés gérées par le service
    - Les fournisseurs de ressources Azure effectuer des opérations de chiffrement et le déchiffrement de hello
    - Microsoft gère les clés de hello
    - Fonctionnalité cloud complète

- Chiffrement côté serveur à l’aide de clés gérées par le client dans Azure Key Vault
    - Les fournisseurs de ressources Azure effectuer des opérations de chiffrement et le déchiffrement de hello
    - Le client contrôle les clés via Azure Key Vault
    - Fonctionnalité cloud complète

- Chiffrement côté serveur à l’aide de clés gérées par le client sur du matériel contrôlé par le client
    - Les fournisseurs de ressources Azure effectuer des opérations de chiffrement et le déchiffrement de hello
    - Le client contrôle les clés sur du matériel contrôlé par le client
    - Fonctionnalité cloud complète

Pour le chiffrement du côté client, tenez compte des éléments suivants de hello :

- Les services Azure ne peuvent pas voir les données déchiffrées
- Les clients gèrent et stockent les clés localement (ou dans d’autres magasins sécurisés). Les clés ne sont pas disponibles tooAzure services
- Fonctionnalité cloud réduite

le chiffrement Hello pris en charge les modèles dans Azure Fractionner en deux groupes principaux : « Chiffrement de Client » et « chiffrement côté serveur », comme indiqué précédemment. Notez que, indépendamment du chiffrement hello au modèle rest des services Azure utilisés recommandons toujours utiliser hello d’un transport sécurisé tel que TLS ou HTTPS. Par conséquent, le chiffrement de transport doit être traité par le protocole de transport hello et ne doit pas être un facteur majeur pour déterminer le chiffrement au toouse de modèle rest.

### <a name="client-encryption-model"></a>Modèle de chiffrement client

Modèle de chiffrement client fait référence à tooencryption est réalisée en dehors de hello Azure ou fournisseur de ressources par un service de hello ou application appelante. le chiffrement Hello peut être effectué par l’application de service hello dans Azure, ou par une application en cours d’exécution dans le centre de données client hello. Dans les deux cas, quand vous tirez parti de ce modèle de chiffrement, hello fournisseur de ressources Azure reçoit un objet blob chiffré des données sans données de hello toodecrypt hello possibilité en aucune façon ou avait des clés de chiffrement toohello accès. Dans ce modèle, la gestion de clés hello est effectuée par hello appel de service ou l’application et est complètement opaque toohello service Azure.

![Client](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>Modèle de chiffrement côté serveur

Modèles de chiffrement côté serveur, reportez-vous à tooencryption est effectuée par hello service Azure. Dans ce modèle, hello fournisseur de ressources effectue hello chiffrer et déchiffrer des opérations. Par exemple, le stockage Azure peut recevoir des données dans les opérations de texte brut et n’effectuera hello chiffrement et déchiffrement en interne. Hello fournisseur de ressources peut utiliser des clés de chiffrement qui sont gérés par Microsoft ou par le client hello selon hello fourni de configuration. 

![Serveur](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Modèles de gestion des clés de chiffrement côté serveur

Chacun de chiffrement du côté serveur hello les modèles rest implique les particularités de gestion de clés. Cela inclut où et comment les clés de chiffrement sont créées et stockées en tant qu’ainsi que les modèles d’accès hello hello les procédures de la rotation des clés. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Chiffrement côté serveur à l’aide de clés gérées par le service

Pour de nombreux clients, hello est exigence essentielle tooensure qui hello des données est chiffré lorsqu’il est au repos. Ce modèle permet de chiffrement côté serveur à l’aide de clés de Service géré en autorisant les clients ressource spécifique toomark hello (compte de stockage, base de données SQL, etc.) pour le chiffrement et de sortie de tous les aspects de la gestion de clés telles que la sauvegarde, de la rotation et de l’émission de la clé tooMicrosoft. La plupart des Services Azure qui prennent en charge le chiffrement au repos généralement prendre en charge ce modèle de gestion hello de tooAzure de clés de chiffrement hello de déchargement. fournisseur de ressources Azure Hello crée des clés de hello, les place dans le stockage sécurisé et récupère en cas de besoin. Cela signifie que le service de hello a clés d’accès complet de toohello service de hello dispose du contrôle total sur la gestion du cycle de vie des informations d’identification hello.

![géré](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

Chiffrement côté serveur à l’aide de clés de service géré par conséquent rapidement des adresses hello besoin toohave chiffrement au repos avec faible toohello charge client. Lorsqu’il est disponible un client ouvre hello portail Azure pour l’abonnement cible de hello et le fournisseur de ressources en général et vérifie une zone indiquant que souhaite hello toobe de données chiffrée. Dans certains gestionnaires de ressources, le chiffrement côté serveur avec des clés gérées par le service est activé par défaut. 

Le chiffrement côté serveur avec les clés gérée par Microsoft implique hello service toostore d’un accès complet et gère les clés de hello. Alors que certains clients peuvent souhaiter des clés de hello toomanage parce qu’elles qu'ils peuvent garantir une plus grande sécurité, hello coût et les risques associés à une solution de stockage de clés personnalisé prenez en compte lors de l’évaluation de ce modèle. Dans de nombreux cas, une organisation peut déterminer que les contraintes de ressources ou des risques liés à une solution sur site peuvent supérieure risque de hello de gestion du cloud de chiffrement hello clés de rest.  Toutefois, ce modèle peut ne pas suffire pour les organisations qui disposent de la création de spécifications toocontrol hello ou cycle de vie des clés de chiffrement hello ou des personnes différentes toohave gérer les clés de chiffrement d’un service que ceux de la gestion du service de hello (c'est-à-dire, répartition des tâches de gestion de clés à partir de hello globale modèle de gestion de service de hello).

##### <a name="key-access"></a>Accès aux clés

Lorsque le chiffrement côté serveur avec des clés de Service géré est utilisé, de création de la clé, hello accès de stockage et de service sont gérés par le service de hello. En règle générale, les fournisseurs de ressources Azure fondamentaux hello stockera hello les clés de chiffrement de données dans un magasin de fermer les données toohello et rapidement disponible et accessible lors des clés de chiffrement de clé hello sont stockés dans un magasin interne sécurisé.

**Avantages**

- Simplicité de la configuration
- Microsoft gère la rotation, la sauvegarde et la redondance des clés
- Client n’a pas hello les coûts d’implémentation ou hello risque d’un schéma personnalisé de gestion de clés.

**Inconvénients**

- Aucun contrôle de client sur les clés de chiffrement hello (spécification de clé, du cycle de vie, révocation, etc.).
- Aucune gestion de clés toosegregate possibilité à partir d’un modèle de gestion globale pour le service de hello

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Chiffrement côté serveur à l’aide de clés gérées par le client dans Azure Key Vault 

Pour les scénarios où la spécification de hello donnée tooencrypt hello au repos et contrôle les clients de clés de chiffrement de hello peuvent utiliser le chiffrement côté serveur à l’aide des clés de client gérés dans le coffre de clés. Certains services peuvent stocker uniquement les racine hello clé de cryptage dans Azure Key Vault et magasin hello chiffrée de clé de chiffrement de données dans les données toohello plus proche d’un emplacement interne. Dans peuvent apporter leurs propres clients de scénario tooKey (BYOK, Bring Your Own Key), le coffre de clés ou générer de nouvelles et utilisez les tooencrypt hello souhaité ressources. Alors que hello fournisseur de ressources effectue les opérations de chiffrement et déchiffrement hello il utilise clé de hello configuré en tant que clé de racine hello pour toutes les opérations de chiffrement. 

##### <a name="key-access"></a>Accès aux clés

Hello modèle de chiffrement côté serveur avec des clés de client géré dans Azure Key Vault implique hello service tooencrypt de clés de l’accès aux hello et déchiffrer selon vos besoins. Chiffrement des clés de rest sont effectuées service tooa accessible via une stratégie de contrôle d’accès l’octroi de cette clé de service identité accès tooreceive hello. Un service Azure s’exécutant pour le compte d’un abonnement associé peut être configuré avec une identité pour ce service au sein de cet abonnement. service de Hello puisse effectuer l’authentification Azure Active Directory et recevoir un jeton d’authentification s’identifie en tant que ce service agissant au nom de l’abonnement de hello. Ce jeton peut ensuite être présenté tooKey coffre tooobtain une clé qu’il a été autorisé à accéder.

Pour les opérations à l’aide de clés de chiffrement, une identité de service peut être accordée tooany accès Hello opérations suivantes : déchiffrer, chiffrer, unwrapKey, wrapKey, vérifier, signer, obtenir, liste, mettre à jour, créer, importer, supprimer, sauvegarder et restaurer.

tooobtain une clé pour une utilisation dans les chiffrer ou déchiffrer des données au niveau de l’identité du service rest hello que hello du Gestionnaire de ressources du service s’exécute doivent avoir UnwrapKey (clé tooget hello pour le déchiffrement) et WrapKey (tooinsert une clé dans le coffre de clés lors de la création d’une nouvelle clé).


>[!NOTE] 
>Pour plus d’informations sur le coffre de clés autorisation Voir hello sécuriser votre page coffre de clés Bonjour [documentation d’Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Avantages**

- Contrôle total sur les clés hello utilisé – chiffrement de clés sont gérées dans le coffre de clés du client hello sous contrôle de code du client hello.
- Capacité tooencrypt maître de tooone plusieurs services
- Détermine la séparation de gestion de clés à partir d’un modèle de gestion globale pour le service de hello
- Possibilité de définir l’emplacement du service et des clés dans des régions différentes

**Inconvénients**

- Le client a l’entière responsabilité de la gestion de l’accès aux clés
- Le client a l’entière responsabilité de la gestion du cycle de vie des clés
- Charge de travail supplémentaire pour l’installation et la configuration

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>Chiffrement côté serveur à l’aide de clés gérées par le service sur du matériel contrôlé par le client

Pour les scénarios où les exigence hello tooencrypt hello de données au repos et gérer des clés de hello dans un référentiel propriétaire en dehors du contrôle de Microsoft, certains services Azure activer le modèle de gestion de clés hello hôte votre propre clé (liées à HYOK). Dans ce modèle, le service de hello doit récupérer la clé de hello à partir d’un site externe et par conséquent, les garanties de disponibilité et les performances sont affectées configuration est plus complexe. En outre, étant donné que le service de hello n’a pas accès toohello DEK au cours du chiffrement de hello et opérations de déchiffrement hello des garanties de sécurité globale de ce modèle sont similaires hello toowhen clés sont gérées par le client dans le coffre de clés Azure.  Par conséquent, ce modèle n’est pas approprié pour la plupart des organisations, sauf si elles ont des exigences spécifiques de gestion des clés qui le nécessitent. En raison des limitations de toothese, la plupart des Services Azure ne gèrent pas le chiffrement côté serveur à l’aide de clés de serveur géré dans le matériel de contrôlés par le client.

##### <a name="key-access"></a>Accès aux clés

Lorsque le chiffrement côté serveur à l’aide de clés de service géré dans le matériel de contrôlés par le client est utilisé hello clés conservées sur un système configuré par le client de hello. Les services Azure qui prennent en charge ce modèle fournissent un moyen de l’établissement d’un client de tooa de connexion sécurisée fournie le magasin de clés.

**Avantages**

- Contrôle total sur la clé racine de hello utilisé – chiffrement de clés sont gérées par un magasin fournis par le client
- Capacité tooencrypt maître de tooone plusieurs services
- Détermine la séparation de gestion de clés à partir d’un modèle de gestion globale pour le service de hello
- Possibilité de définir l’emplacement du service et des clés dans des régions différentes

**Inconvénients**

- Entière responsabilité pour le stockage, la sécurité, les performances et la disponibilité des clés
- Entière responsabilité de la gestion de l’accès aux clés
- Entière responsabilité de la gestion du cycle de vie des clés
- Coûts considérables d’installation, de configuration et de maintenance
- Dépendance accrue sur la disponibilité du réseau entre le centre de données client hello et des centres de données Azure.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Chiffrement au repos dans les services cloud Microsoft

Les services cloud Microsoft sont utilisés dans chacun des trois modèles cloud : IaaS, PaaS, SaaS. Voici des exemples de la façon dont ils s’adaptent sur chaque modèle :

- Services logiciels, tooas référencé logiciel en tant que serveur ou SaaS, ayant une application fournie par le cloud hello tels qu’Office 365.
- Les clients qui exploitent cloud hello dans leurs applications, à l’aide de cloud de hello pour les opérations des services de plateforme, tels que les fonctionnalités de bus de stockage, analytique et le service.
- Services d’infrastructure ou d’Infrastructure en tant que Service (IaaS) dans les clients de déployer des systèmes d’exploitation et les applications qui sont hébergées dans hello cloud et éventuellement tirant parti des autres services de cloud computing.

### <a name="encryption-at-rest-for-saas-customers"></a>Chiffrement au repos pour les clients SaaS

Les clients SaaS (Software as a Service) ont généralement le chiffrement au repos activé ou disponible dans chaque service. Les services Office 365 propose plusieurs options pour le chiffrement tooverify ou activer des clients au repos. Pour plus d’informations sur les services Office 365, consultez Technologies de chiffrement des données pour Office 365.

### <a name="encryption-at-rest-for-paas-customers"></a>Chiffrement au repos pour les clients PaaS

Plateforme en tant que données d’un client de Service (PaaS) se trouve généralement dans un environnement d’exécution d’applications et les fournisseurs de ressources Azure utilisé toostore les données des clients. chiffrement de hello toosee à tooyou disponibles des options de rest examiner de plateformes de stockage et l’application hello que vous utilisez le tableau hello ci-dessous. Prise en charge, tooinstructions des liens sur l’activation du chiffrement au repos sont fournies pour chaque fournisseur de ressources. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Chiffrement au repos pour les clients IaaS

Les clients IaaS (Infrastructure as a Service) peuvent utiliser différents services et applications. Les services IaaS peuvent activer le chiffrement au repos dans leurs machines virtuelles et leurs disques durs virtuels hébergés dans Azure en utilisant Azure Disk Encryption. 

#### <a name="encrypted-storage"></a>Stockage chiffré

Comme pour PaaS, les solutions IaaS peuvent tirer parti d’autres services Azure qui stockent les données chiffrées au repos. Dans ce cas, vous pouvez activer hello chiffrement au niveau de prise en charge Rest tel que fourni par chaque service Azure utilisé. Hello tableau ci-dessous énumère le stockage hello, services et plateformes d’application et le modèle de hello de chiffrement au repos pris en charge. Prise en charge, des liens sont fournis tooinstructions sur l’activation du chiffrement au repos. 

#### <a name="encrypted-compute"></a>Calcul chiffré

Un chiffrement complet à la solution de Rest nécessite que hello données ne sont jamais conservées sous forme non chiffrée. En cours d’utilisation, application peut effectuer sur un hello lors du chargement de serveur les données en mémoire, les données peuvent être rendu persistant localement de différentes manières, y compris le fichier d’échange Windows hello, un vidage sur incident et n’importe quel enregistrement Bonjour. tooensure ces données sont chiffrées au repos applications IaaS peuvent utiliser le chiffrement de disque Azure sur une machine virtuelle de IaaS Azure (Windows ou Linux) et le disque virtuel. 

#### <a name="custom-encryption-at-rest"></a>Chiffrement au repos personnalisé

Il est recommandé que, chaque fois que c’est possible, les applications IaaS tirent parti des options d’Azure Disk Encryption et du chiffrement au repos fournies par les services Azure utilisés. Dans certains cas, tels que les exigences de chiffrement irrégulières ou de stockage basé sur non-Azure, un développeur d’une application IaaS peut être nécessaire de chiffrement tooimplement au rest eux-mêmes. Les développeurs de solutions IaaS peuvent mieux s’intégrer à la gestion d’Azure et répondre aux attentes des clients en tirant parti de certains composants Azure. Plus précisément, les développeurs doivent utiliser hello Azure Key Vault service tooprovide sécuriser le stockage de la clé ainsi que proposer à leurs clients avec les options de gestion de clé cohérent avec celui des services de plateforme Azure plus. En outre, des solutions personnalisées doivent utiliser des clés de chiffrement d’identités de Service Azure Managed tooenable service comptes tooaccess. Pour plus d’informations sur Azure Key Vault et les identités de service gérées, les développeurs peuvent consulter leurs SDK respectifs.

## <a name="azure-resource-providers-encryption-model-support"></a>Prise en charge du modèle de chiffrement des fournisseurs de ressources Azure

Microsoft Azure chaque prennent en charge un ou plusieurs de chiffrement hello les modèles rest. Pour certains services, toutefois, une ou plusieurs des modèles de chiffrement hello peut-être pas applicable. En outre, les services peuvent prendre en charge ces scénarios selon des planifications différentes. Cette section décrit le chiffrement au niveau de prise en charge de rest lors de ce document pour chacun des services de stockage de données Azure principaux hello hello hello.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Tout client utilisant les fonctionnalités IaaS d’Azure peut effectuer le chiffrement au repos pour ses machines virtuelles et ses disques IaaS via Azure Disk Encryption. Pour plus d’informations sur le disque de Azure chiffrement voir hello [documentation de chiffrement de disque Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Stockage Azure

Les services Azure Stockage Blob et Stockage Fichier prennent en charge le chiffrement au repos pour les scénarios avec chiffrement côté serveur, ainsi que les données chiffrées par le client (chiffrement côté client).

- Côté serveur : les clients utilisant Azure Stockage Blob peuvent activer le chiffrement au repos sur chaque compte de ressource de stockage Azure. Le chiffrement côté serveur après l’activation s’effectue en toute transparence toohello application. Pour plus d’informations, consultez [Azure Storage Service Encryption pour les données au repos](https://docs.microsoft.com/azure/storage/storage-service-encryption).
- Côté client : le chiffrement côté client des objets blob Azure est pris en charge. Lorsque vous utilisez le chiffrement côté client clients chiffrement hello des données et les données hello comme un objet blob chiffré. Gestion de clés est effectuée par le client de hello. Pour plus d’informations, consultez [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).


#### <a name="sql-azure"></a>SQL Azure

Azure SQL Database prend actuellement en charge le chiffrement au repos pour les scénarios de chiffrement côté service géré par Microsoft et côté client.

Serveur de prise en charge de chiffrement est actuellement fourni via la fonctionnalité SQL hello appelée chiffrement Transparent des données. Une fois qu’un client Azure SQL Database active Transparent Data Encryption, les clés sont créées et gérées automatiquement pour lui. Chiffrement au repos peut être activé à des niveaux de base de données et serveur hello. À compter de juin 2017, [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) est activé par défaut sur les bases de données nouvellement créées.

Le chiffrement côté client de données SQL Azure est prise en charge par le biais hello [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) fonctionnalité. Chiffrement intégral utilise une clé qui a créé et stocké par le client de hello. Clients peuvent stocker la clé principale de hello dans un magasin de certificats Windows, Azure Key Vault ou un Module de sécurité matériel local. À l’aide de SQL Server Management Studio, les utilisateurs choisissent les éléments clés souhaite toouse tooencrypt quelle colonne.

|                                  |                |                     | **Modèle de chiffrement**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **Client** |
|                                  | **Gestion des clés** | **Clé gérée par le service** | **Gérée par le client dans un coffre de clés** | **Gérée par le client localement** |        |
| **Stockage et bases de données**            |                |                     |                              |                              |        |
| Disque (IaaS)                      |                | -                   | Oui                          | Oui*                         | -      |
| SQL Server (IaaS)                |                | Oui                 | Oui                          | Oui                          | Oui    |
| Azure SQL Database (PaaS)                 |                | Oui                 | VERSION PRÉLIMINAIRE                      | -                            | Oui    |
| Stockage Azure (Objets blob de blocs/pages) |                | Oui                 | VERSION PRÉLIMINAIRE                      | -                            | Oui    |
| Stockage Azure (Fichiers)            |                | Oui                 | -                            | -                            | -      |
| Stockage Azure (Tables, Files d’attente)   |                | -                   | -                            | -                            | Oui    |
| Cosmos DB (Document DB)          |                | Oui                 | -                            | -                            | -      |
| StorSimple                       |                | Oui                 | -                            | -                            | Oui    |
| Sauvegarde                           |                | -                   | -                            | -                            | Oui    |
| **Décisionnel &amp; Analytique**       |                |                     |                              |                              |        |
| Azure Data Factory               |                | Oui                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | VERSION PRÉLIMINAIRE                      | -                            | -      |
| Azure Stream Analytics           |                | Oui                 | -                            | -                            | -      |
| HDInsights (Stockage Blob Azure)  |                | Oui                 | -                            | -                            | -      |
| HDInsights (Stockage Data Lake)   |                | Oui                 | -                            | -                            | -      |
| Azure Data Lake Store            |                | Oui                 | Oui                          | -                            | -      |
| Azure Data Catalog               |                | Oui                 | -                            | -                            | -      |
| Power BI                         |                | Oui                 | -                            | -                            | -      |
| **Services IoT**                     |                |                     |                              |                              |        |
| IoT Hub                          |                | -                   | -                            | -                            | Oui    |
| Service Bus                      |                | -              | -                            | -                            | Oui    |
| Event Hubs                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Conclusion

Protection des données client stockées dans les Services Azure est d’une importance capitale tooMicrosoft. Hébergé de Azure tous les services sont validé tooproviding chiffrement au niveau des options de Rest. Les services fondamentaux, comme Stockage Azure, Azure SQL Database, et les services clés de décisionnel et d’analytique, offrent déjà des options de chiffrement au repos. Certains de ces services prennent en charge les clés contrôlées par le client ou le chiffrement côté client, ainsi que les clés et le chiffrement gérés par le service. Services Microsoft Azure sont largement amélioration de chiffrement au niveau de disponibilité de Rest et de nouvelles options sont planifiées pour afficher un aperçu et de la disponibilité générale dans les mois à venir hello.

