---
title: aaaData Classification pour Azure | Documents Microsoft
description: "Cet article fournit une présentation toohello notions de base de la classification des données et met en surbrillance de sa valeur, en particulier dans le contexte de hello de cloud computing et à l’aide de Microsoft Azure"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Classification des données pour Azure
Cet article fournit une présentation toohello notions de base de la classification des données et met en évidence de sa valeur, en particulier dans le contexte de hello de cloud computing et à l’aide de Microsoft Azure. 

## <a name="data-classification-fundamentals"></a>Principes fondamentaux de la classification des données
Une classification des données réussie au d’une organisation requiert une large reconnaissance de vos besoins et une connaissance approfondie de l’emplacement de vos ressources de données.  

Les données peuvent être : 

* Au repos 
* En cours de traitement 
* En transit 

Les trois états nécessitent des solutions techniques uniques pour la classification des données, mais hello principes appliqués de classification des données doit être hello même pour chacun. Données qui sont classées comme confidentielles doivent toostay confidentielles au repos, dans le processus et en transit. 

Les données peuvent également être structurées ou non structurées. Processus de classification classique pour hello structuré de données que se trouvent dans des bases de données et des feuilles de calcul sont moins complexe et long toomanage que celles des données non structurées, telles que la messagerie, de code source et de documents. 

> [!TIP]
> Pour plus d’informations sur les fonctionnalités d’Azure et les bonnes pratiques relatives au chiffrement des données, consultez [Bonnes pratiques relatives au chiffrement des données Azure](azure-security-data-encryption-best-practices.md).
> 
> 

En règle générale, les organisations disposent d’un nombre plus important de données non structurées que de données structurées. Indépendamment de si les données sont structurées ou non, il est important de sensibilité données toomanage. Lorsqu’elle est correctement implémentée, la classification des données permet de garantir que les données sensibles ou confidentielles actifs sont gérés avec supervision supérieure à des ressources de données qui sont considérés comme toodistribute public ou libre. 

### <a name="controlling-access-toodata"></a>Contrôle d’accès toodata
Authentification et autorisation sont souvent confondues et leurs rôles mal compris. En réalité qu’ils sont très différents, comme indiqué dans la figure suivante de hello.  

![Accès aux données et contrôle](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Authentification
L’authentification est généralement constitué d’au moins deux parties : un tooidentify ID utilisateur ou le nom d’utilisateur un utilisateur et un jeton, comme un mot de passe tooconfirm qui hello des informations d’identification de nom d’utilisateur est valide. processus de Hello ne fournit pas d’utilisateur authentifié de hello avec accès tooany éléments ou des services ; Il vérifie que l’utilisateur hello est ceux qu’ils prétendent qu'être.   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md) fournit des services d’identité basé sur le cloud qui vous tooauthenticate et autorisent les utilisateurs. 
> 
> 

### <a name="authorization"></a>Autorisation
L’autorisation est processus hello en fournissant une tooaccess de capacité hello utilisateur authentifié une application, jeu de données, fichier de données ou un autre objet. Affectation d’utilisateurs authentifiés hello droits toouse, modifier ou supprimer les éléments auxquels ils peuvent accéder requiert la classification de toodata une attention particulière. 

Autorisation réussie requiert l’implémentation d’un mécanisme toovalidate des utilisateurs doit tooaccess fichiers et des informations basées sur une combinaison de rôle, la stratégie de sécurité et considérations relatives à la stratégie risque. Par exemple, les données à partir des applications line-of-business (LOB) spécifiques n’est peut-être pas toobe accessible par tous les employés, et seul un petit sous-ensemble d’employés aura probablement besoin d’accès toohuman les fichiers de ressources (h). Mais pour les organisations toocontrol qui peut accéder aux données, ainsi que quand et comment, un système efficace pour authentifier les utilisateurs doit être en place. 

> [!TIP]
> dans Microsoft Azure, assurez-vous que tooleverage du contrôle d’accès (RBAC) toogrant que hello quantité d’accès que les utilisateurs doivent tooperform leur travail. Lecture [utiliser des ressources Azure Active Directory de rôle affectations toomanage accès tooyour](../active-directory/role-based-access-control-configure.md) pour plus d’informations. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Rôles et responsabilités du cloud computing
Bien que les fournisseurs de cloud peuvent aider à gérer les risques, les clients doivent tooensure cette gestion de classification des données et l’application est correctement implémentée tooprovide hello appropriés au niveau des services de gestion de données.  

Classification des données responsabilités varie selon le modèle de service cloud est en place, comme indiqué dans la figure suivante de hello. trois modèles de service cloud principal Hello sont infrastructure en tant que service (IaaS), plateforme en tant que service (PaaS) et le logiciel en tant que service (SaaS). Implémentation de mécanismes de classification des données sera également varie en fonction envers les hello et des attentes de fournisseur de cloud hello. 

![contrôleur](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Bien que vous êtes responsable pour classifier vos données, fournisseurs de cloud doivent rendre des engagements écrites sur comment ils sécuriser et préserver la confidentialité hello des données de client hello stockées dans le cloud.  

* **Les fournisseurs IaaS** exigences sont limités tooensuring qui hello environnement virtuel peut prendre en charge les fonctionnalités de classification des données et les exigences de conformité de client. Les fournisseurs IaaS ont un rôle plus petit dans la classification des données, car il leur suffit de tooensure que les données client répond aux exigences de conformité. Toutefois, les fournisseurs doivent tout en garantissant que leurs environnements virtuels adresse les exigences de classification des données dans Ajout toosecuring leurs centres de données.
* **Les fournisseurs de services PaaS** responsabilités peuvent être mélangées, car la plate-forme de hello peut être utilisée dans une sécurité de tooprovide approche en couches pour un outil de classification. Fournisseurs de PaaS peuvent être chargés pour l’authentification et éventuellement des règles d’autorisation et il doivent fournir sécurité et la couche d’application tootheir données classification fonctionnalités. Beaucoup tout comme les fournisseurs IaaS, PaaS fournisseurs ont besoin de tooensure leur plate-forme conforme avec des exigences de classification des données pertinentes.
* **Les fournisseurs SaaS** sont souvent considérés comme faisant partie d’une chaîne d’autorisation, et sera peut-être tooensure qui hello des données stockées dans une application SaaS de hello peut être contrôlé par le type de classification. Applications SaaS peuvent être utilisées pour les applications métier, et par leur nature devez tooprovide hello signifie tooauthenticate et autoriser les données qui sont utilisées et stockées. 

## <a name="classification-process"></a>Processus de classification
De nombreuses organisations qui comprennent hello nécessaire à la classification des données et souhaitez tooimplement sont confrontés à une authentification de base : où toobegin ?

Une façon simple et efficace de classification des données tooimplement est toouse hello PLAN, faire, vérification, acte de modèle à partir de [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). suivant de Hello figure graphiques tâches hello de classification des données implémentent toosuccessfully requis dans ce modèle.  

1. **PRÉVOIR**. Identifier les ressources de données, un programme de classification de données opérateur toodeploy hello et développer les profils de protection. 
2. **DÉPLOYER**. Une fois les stratégies de classification des données sont convenus, déployer hello programme et à implémenter des technologies de mise en œuvre en fonction des besoins pour les données confidentielles.  
3. **VÉRIFIER**. Vérifiez et validez les rapports tooensure outils de hello et méthodes utilisés efficacement traitez hello des stratégies de classification. 
4. **AGIR**. Examinez l’état hello d’accès aux données et consulter les fichiers et les données qui nécessitent une révision à l’aide d’un reclassement et modifications de révision méthodologie tooadopt et tooaddress nouveaux risques.  

![Plan, do, Check, Act (Prévoir, déployer, vérifier et agir)](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Sélectionner un modèle de terminologie qui répond à vos besoins.
Il existe plusieurs types de processus pour la classification des données, y compris des processus manuels, processus basée sur l’emplacement pour classer les données en fonction de l’emplacement du système ou d’un utilisateur, les processus d’application telles que la classification de la base de données spécifiques et automatisée processus utilisés par les différentes technologies, dont certaines sont décrites dans la section de « Protection des données confidentielles » hello plus loin dans cet article.  

Cet article présente deux modèles de terminologie généralisés reposant sur des modèles bien utilisés et respectés dans le secteur. Ces modèles de terminologie, qui fournissent trois niveaux de sensibilité de la classification, sont affichés dans hello tableau suivant.  

> [!NOTE]
> lors de la classification d’un fichier ou une ressource que combine les données qui sont généralement classées à différents niveaux, hello plus haut niveau de classification présent doivent établir hello classification globale. Par exemple, un fichier contenant des données sensibles ou limitées doit être classé comme restreint.  
> 
> 

| **Sensibilité** | **Modèle de terminologie 1** | **Modèle de terminologie 2** |
| --- | --- | --- |
| Élevé |Confidentiel |Restreint |
| Moyenne |À usage interne uniquement |Sensible |
| Faible |Public |Non restreint |

#### <a name="confidential-restricted"></a>Confidentiel (limité)
Informations sont classées comme confidentiel ou restreint incluent des données qui peuvent être tooone catastrophique ou que plusieurs personnes et/ou organisations en cas de perte ou de compromis. Ces informations sont fournies fréquemment une base « tooknow nécessaire » et peuvent inclure : 

* Des données personnelles, notamment des informations d’identification personnelle, telles que des numéros de sécurité sociale ou de carte d’identité, de passeport, de carte de crédit, de permis de conduire, de dossier médical et d’assurance maladie.  
* Des données financières, notamment des numéros de compte financier, tels que des numéros de compte bancaire ou d’investissement. 
* Des documents professionnels, tels que des documents ou des données uniques ou soumis à la propriété intellectuelle.  
* Des données juridiques, notamment des documents d’avocat potentiellement confidentiels. 
* Des données d’authentification, notamment des clés de chiffrement privées, des combinaisons nom d’utilisateur/mot de passe ou d’autres séquences d’identification, telles que des fichiers de clés biométriques privées. 

Les données classées comme confidentielles sont souvent soumises à des exigences réglementaires et de conformité en matière de gestion des données. 

#### <a name="for-internal-use-only-sensitive"></a>À usage interne uniquement (sensible)
Les informations classées comme étant de sensibilité moyenne incluent les fichiers et les données, dont la perte ou la destruction n’aurait pas d’impact majeur sur une organisation et/ou un individu. Ces informations peuvent inclure les éléments suivants : 

* Courrier électronique, la plupart d'entre eux peut être supprimée ou distribuée sans entraîner une situation de crise (à l’exclusion des boîtes aux lettres ou par courrier électronique de personnes qui sont identifiées dans la classification de confidentiel hello).  
* Les documents et les fichiers qui n’incluent pas de données confidentielles.

En général, cette classification inclut tout ce qui n’est pas confidentiel. Cette classification peut inclure la plupart des données d’entreprise, dans la mesure où la plupart des fichiers gérés ou utilisés quotidiennement peuvent être classés comme sensibles. Avec l’exception hello de données sont rendues publique ou confidentielles, toutes les données dans une organisation de l’entreprise peuvent être classées comme sensibles par défaut. 

#### <a name="public-unrestricted"></a>Public (non restreint)
Informations sont classifiées comme étant public incluent les données et les fichiers qui ne sont pas critiques toobusiness besoins ou opérations. Cette classification peut également inclure des données qui ont été délibérément finale toohello public pour leur utilisation, telles que la commercialisation des annonces de matériel ou appuyez sur. En outre, cette classification peut inclure des données, telles que des courriers indésirables stockés par un service de messagerie. 

### <a name="define-data-ownership"></a>Définir la propriété des données
Il est important tooestablish une chaîne désactivez garde de possession pour toutes les ressources de données. Hello tableau suivant identifie les rôles de la propriété des données différentes dans les efforts de classification des données et leurs droits respectifs.  

| **Rôle** | **Créer** | **Modifier/supprimer** | **Déléguer** | **Lire** | **Archiver/restaurer** |
| --- | --- | --- | --- | --- | --- |
| Propriétaire |X |X |X |X |X |
| Opérateur | | |X | | |
| Administrateur | | | | |X |
| Utilisateur\* | |X | |X | |

**Les utilisateurs peuvent également bénéficier de droits supplémentaires, comme la modification et la suppression par un opérateur* 

> [!NOTE]
> ce tableau ne fournit pas de liste exhaustive des rôles et des droits, mais simplement un échantillon représentatif. 
> 
> 

Hello **propriétaire de la ressource** est hello le créateur d’origine des données hello, qui peuvent déléguer l’appartenance et affecter un opérateur. Lorsqu’un fichier est créé, propriétaire de hello doit être en mesure de tooassign une classification, ce qui signifie qu’ils ont une toounderstand responsabilité en ce qui doit toobe classée comme confidentielles basées sur des stratégies de leur organisation. Toutes les données d’un propriétaire de ressources de données peuvent être classées automatiquement comme étant à usage interne uniquement (sensible) à moins qu’il ne soit chargé de l’appartenance ou de la création de types de données confidentielles (restreintes). Rôle de propriétaire hello modifiera fréquemment, une fois que les données de salutation sont classées. Par exemple, propriétaire de hello peut créer une base de données de classification des informations et abandonner leur conservateur de données toohello droits.  

> [!NOTE]
> les propriétaires de données asset utilisent souvent un mélange de services, périphériques et les médias, dont certains sont personnelles et certains d'entre eux appartiennent toohello organisation. Une stratégie d’organisation clairement établie peut permettre de garantir que l’utilisation d’appareils, tels que des ordinateurs portables et des appareils intelligents est en conformité avec les directives relatives à la classification des données.  
> 
> 

Hello **conservateur actifs de données** ou est attribué par le propriétaire de la ressource hello (ou leur délégué) toomanage hello asset conséquente tooagreements avec le propriétaire de la ressource hello conformément aux exigences de la stratégie applicable. Dans l’idéal, le rôle d’opérateur hello peut être implémentée dans un système automatisé. Un opérateur asset garantit que des contrôles d’accès nécessaires sont fournis et est responsables de la gestion et protection des ressources déléguées tootheir soins. responsabilités Hello d’opérateur d’élément multimédia hello sont les suivantes :  

* Protection de la ressource hello en fonction de la direction du propriétaire de la ressource hello ou propriétaire de la ressource hello en accord avec 
* Garantir le respect des stratégies de classification 
* Pour informer les propriétaires des ressources de n’importe quel change tooagreed-lors des contrôles et/ou des modifications de toothose préalable de procédures de protection prise d’effet 
* Propriétaire de la ressource toohello création de rapports sur la suppression de tooor modifications les responsabilités d’opérateur hello actif 
* Un **administrateur** représente un utilisateur chargé de s’assurer du maintien de l’intégrité, mais n’est pas un propriétaire de la ressource de données, un opérateur ou un utilisateur. En fait, plusieurs rôles d’administrateur fournissent des services de gestion de conteneur de données sans devoir accéder à des données toohello. rôle d’administrateur Hello inclut la sauvegarde et restauration des données hello, gestion des enregistrements de ressources de hello, et en choisissant, lors de l’acquisition et l’exploitation hello appareils et stockage qu’actifs de hello maison. 
* utilisateur actif de Hello inclut tout le monde auquel est accordé l’accès toodata ou un fichier. Affectation de l’accès est souvent déléguée par l’opérateur de hello propriétaire toohello actif.  

### <a name="implementation"></a>Implémentation
Considérations relatives à la gestion s’appliquent les méthodologies de classification tooall. Ces considérations doivent tooinclude des détails concernant les personnes, ce qui, où, quand et pourquoi une ressource de données serait être utilisée, accessible, modifiée ou supprimée. Toute la gestion des actifs est indispensable de comprendre comment une organisation consulte les risques, mais une méthodologie simple peut être appliquée comme défini dans le processus de classification des données hello. Considérations supplémentaires pour la classification de données incluent des introduction hello de nouvelles applications et les outils et la gestion des modifications après l’implémentation d’une méthode de classification.  

### <a name="reclassification"></a>Reclassification
Reclassement ou la modification d’état de classification hello d’une ressource de données doit toobe effectuée lorsqu’un utilisateur ou système détermine l’importance de ce hello données d’élément multimédia ou le profil de risque a changé. Cet effort est importante pour s’assurer que le statut de classification hello continue toobe actuel et valide. La plupart du contenu non classé manuellement peut l’être automatiquement ou en fonction de son utilisation par un opérateur ou propriétaire de données. 

### <a name="manual-data-reclassification"></a>Reclassification manuelle des données
Dans l’idéal, cet effort assureriez que hello les détails d’une modification capturées et auditées. raison la plus probable pour reclassement manuel Hello serait pour des raisons de respect de l’ou des enregistrements conservés dans le format de papier ou une exigence tooreview des données qui a été classées à l’origine. Car cet article considère que la classification des données et déplacement données toohello dans le cloud, les efforts de reclassification manuelle nécessite l’attention sur un cas par cas et une analyse des risques serait idéale tooaddress les exigences de classification. En règle générale, cet un effort serait hello stratégie de l’organisation sur les étapes requises toobe classé de prendre en compte, hello état de classification par défaut (toutes les données et fichiers qui sont sensibles mais non confidentielles) et prendre des exceptions pour les données à haut risque. 

### <a name="automatic-data-reclassification"></a>Reclassification automatique des données
Reclassement de données automatique utilise hello général même règle en tant que la classification manuelle. exception de Hello est que les solutions automatisées peuvent vous assurer que les règles sont suivies et appliqués en fonction des besoins. La classification des données peut être effectuée dans le cadre d’une stratégie de mise en œuvre de la classification de données, qui peut être appliquée lors du stockage, de l’utilisation et du transit des données à l’aide de la technologie d’autorisation.

* En fonction d’une application. Un niveau de classification est défini à l’aide de certaines applications par défaut. Par exemple, les données du logiciel de gestion de la relation client (CRM), des ressources humaines et des outils de gestion des dossiers médicaux sont confidentiels par défaut. 
* En fonction d’un emplacement. L’emplacement des données peut permettre d’identifier la sensibilité des données. Par exemple, les données stockées par une ressources humaines ou le service financier sont probablement toobe de caractère confidentiel.  

### <a name="data-retention-recovery-and-disposal"></a>Rétention, récupération et élimination des données
La récupération et l’élimination des données, telles que leur reclassification, sont un aspect essentiel de la gestion des ressources de données. Hello principes pour la récupération des données et l’élimination serait définies par une stratégie de rétention de données et appliquée hello même manière que le reclassement des données ; un effort de ce type serait exécuté par les rôles d’administrateur et opérateur hello comme une tâche de collaboration.  

Échec toohave une stratégie de rétention de données peut signifier toocomply de perte ou de défaillance de données avec les exigences juridiques et réglementaires découverte. La plupart des organisations qui n’ont pas d’une stratégie de rétention des données clairement définis ont tendance à toouse une stratégie de rétention par défaut « conserver tous les éléments ». Toutefois, une telle stratégie de rétention comporte des risques supplémentaires dans des scénarios de services cloud. 

Par exemple, une stratégie de rétention de données pour les fournisseurs de services cloud peut être considéré comme que pour « durée hello d’abonnement de hello » (tant que service de hello est payé pour, les données de salutation sont conservées). Tel un accord de rétention lié au paiement peut ne pas convenir aux stratégies de rétention réglementaires ou d’entreprise. La définition d’une stratégie pour les données confidentielles peut garantir un stockage et une suppression des données selon les meilleures pratiques. En outre, une stratégie d’archivage peut être créée tooformalize comprendre les données doit être supprimé et à quel moment. 

Stratégie de rétention de données doit répondre hello requis réglementaires et les exigences de conformité, ainsi que les exigences de conservation légale d’entreprise. Les données classées peuvent susciter des questions sur la durée de rétention et les exceptions liées aux données stockées auprès d’un fournisseur. De telles questions se poseront plus probablement pour les données n’ayant pas fait l’objet d’une classification correcte. 

> [!TIP]
> en savoir plus sur les stratégies de rétention de données Azure et plus en lisant hello [contrat d’abonnement en ligne Microsoft](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Protection des données confidentielles
Une fois que les données sont classées, recherche et la mise en œuvre de tooprotect des données confidentielles devient partie intégrante de toute stratégie de déploiement de protection de données. Protection des données confidentielles requiert des données de toohow une attention particulière sont stockées et transmises dans des architectures conventionnelles ainsi dans cloud de hello. 

Cette section fournit des informations de base des technologies permettant d’automatiser les efforts de mise en œuvre toohelp protéger les données qui ont été classifiées comme confidentielles. 

Comme la figure suivante présente de hello, ces technologies peuvent être déployés en tant que solutions cloud ou local, ou en mode hybride, avec certaines de ces déployé localement et dans le cloud de hello. (Certaines technologies, telles que le chiffrement et la gestion des droits, également étendent les appareils toouser.)  

![Technologies](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Logiciel de gestion des droits
Le logiciel de gestion des droits est une solution permettant d’empêcher la perte de données. Contrairement aux approches qui tentent de flux de hello toointerrupt d’informations en provenance d’une organisation, le logiciel de gestion des droits fonctionne à des niveaux approfondies dans les technologies de stockage de données. Les documents sont chiffrés et la vérification des personnes autorisées à les déchiffrer utilise les contrôles d’accès définis dans une solution de contrôle d’authentification, tel qu’un service d’annuaire.  

> [!TIP]
> Vous pouvez utiliser Azure Rights Management (Azure RMS) comme données hello informations protection solution tooprotect dans différents scénarios. Pour en savoir plus sur cette solution Azure, consultez [What is Azure Rights Management?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) (Présentation d’Azure Rights Management).
> 
> 

Voici quelques-uns des avantages de hello du logiciel de gestion des droits : 

* Sauvegarde des informations sensibles. Les utilisateurs peuvent protéger leurs données directement à l’aide d’applications compatibles avec la gestion des droits. Aucune étape supplémentaire n’est requise. La création de documents, l’envoi d’e-mails et la publication de données bénéficient d’une protection cohérente des données. 
* Protection se déplace avec les données de salutation. Les clients restent dans le contrôle de l’accès aux données de tootheir, hello infrastructure de cloud computing, existant, ou au bureau de l’utilisateur hello. Les organisations peuvent choisir tooencrypt leurs données et restreindre l’accès en fonction des besoins de l’entreprise tootheir. 
* Stratégies de protection des informations par défaut. Les administrateurs et les utilisateurs peuvent utiliser des stratégies standard pour de nombreux scénarios d’entreprise courants, de type « Confidentiel entreprise - Lecture seule » et « Ne pas transférer ». Un ensemble de droits d’utilisation sont prises en charge telles que la lecture, copier, imprimer, enregistrer, modifier et transmettre tooallow de souplesse dans la définition des droits d’utilisation personnalisés. 

> [!TIP]
> Vous pouvez protéger les données dans Stockage Azure à l’aide d’[Azure Storage Service Encryption](../storage/storage-service-encryption.md) pour les données au repos. Vous pouvez également utiliser [chiffrement de disque Azure](azure-security-disk-encryption.md) toohelp protéger les données contenues sur les disques virtuels utilisés pour les Machines virtuelles Azure.
> 
> 

### <a name="encryption-gateways"></a>Passerelles de chiffrement
Passerelles de chiffrement de fonctionnent dans leurs propres services de chiffrement de couches tooprovide par redirection de toutes les données de toocloud accès. Cette approche ne doit pas être confondue avec celle d’un réseau privé virtuel (VPN). Passerelles de chiffrement sont conçu tooprovide un transparent toocloud les solutions de couche.   

Passerelles de chiffrement peuvent fournir un moyen toomanage et sécuriser les données qui a été classées comme confidentielles en chiffrant les données hello en transit, ainsi que des données au repos.  

Passerelles de chiffrement sont placés dans hello des flux de données entre les appareils d’utilisateur et les services de chiffrement/déchiffrement tooprovide les centres de données d’application. Ces solutions, comme les réseaux privés virtuels, sont majoritairement des solutions sur site. Ils sont conçu tooprovide une tierce partie avec un contrôle sur les clés de chiffrement, qui vous aide à réduire les risques de hello de placer les données de salutation et de gestion de clés avec le fournisseur. Ces solutions sont conçues, comme le chiffrement, toowork en toute transparence entre les utilisateurs et de service de hello. 

> [!TIP]
> Vous pouvez utiliser Azure ExpressRoute tooextend vos réseaux locaux dans le cloud de Microsoft hello sur une connexion privée dédiée. Pour plus d’informations sur cette fonctionnalité, consultez [ExpressRoute - Aperçu technique](../expressroute/expressroute-introduction.md). Une autre option pour une connectivité croisée entre votre réseau local et [Azure est une connexion VPN de site à site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Prévention contre la perte de données
Perte de données (parfois désignée tooas les fuites de données) est un facteur important, et prévention hello de perte de données externes via initiés malveillantes et accidentelles est primordiale pour de nombreuses organisations.  

Les technologies de prévention contre la perte de données peuvent permettre de s’assurer que des solutions, telles que des services de messagerie, ne transmettent pas de données classées comme confidentielles. Les organisations peuvent tirer parti des fonctionnalités DLP dans les produits existant toohelp éviter la perte de données. Ces fonctionnalités utilisent des stratégies qui peuvent être facilement créés de toutes pièces ou à l’aide d’un modèle fourni par le fournisseur de logiciel hello.  

Les technologies DLP peuvent effectuer l’analyse approfondie du contenu de correspondances de mots-clés, de correspondances de dictionnaire, d’évaluation d’expression régulière et autre contenu toodetect examen de contenu qui enfreint les règles DLP d’organisation. Par exemple, DLP peut aider à éviter la perte de hello Hello les types de données suivants : 

* Numéros de sécurité sociale et de carte d’identité 
* Informations bancaires 
* Numéros de carte de crédit  
* Adresses IP 

Certaines technologies DLP fournissent également la configuration de DLP hello capacité toooverride hello (par exemple, si une organisation a besoin de processeur de paie tooa tootransmit numéro de sécurité sociale information). En outre, il est possible tooconfigure DLP afin que les utilisateurs sont avertis avant de tenter de même toosend des informations sensibles qui ne doivent pas être transmises. 

> [!TIP]
> Vous pouvez utiliser Office 365 DLP fonctionnalités tooprotect vos documents. Pour en savoir plus, consultez [Office 365 compliance controls: Data Loss Prevention](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) (Contrôles de conformité Office 365 : prévention contre la perte de données).
> 
> 

## <a name="see-also"></a>Voir aussi
* [Bonnes pratiques en matière de chiffrement des données Azure](azure-security-data-encryption-best-practices.md)
* [Bonnes pratiques en matière de sécurité du contrôle d’accès et de la gestion des identités Azure](azure-security-identity-management-best-practices.md)
* [Blog de l’équipe de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)
* [Centre de réponse aux problèmes de sécurité Microsoft](https://technet.microsoft.com/library/dn440717.aspx)

