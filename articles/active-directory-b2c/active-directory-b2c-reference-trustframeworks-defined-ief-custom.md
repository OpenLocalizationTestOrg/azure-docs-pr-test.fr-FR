---
title: "Azure Active Directory B2C : informations de référence sur les infrastructures de confiance | Microsoft Docs"
description: "Une rubrique sur les stratégies personnalisées Azure Active Directory B2C et hello infrastructure expérience d’identité"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Définir des infrastructures de confiance avec l’infrastructure d’expérience d’identité Azure AD B2C

Azure B2C Active Directory (B2C Active Directory de Azure) des stratégies personnalisées qui utilisent hello identité expérience Framework fournissent à votre organisation avec un service centralisé. Ce service simplifie de hello de fédération d’identité dans une grande Communauté d’intérêt. la complexité de Hello est réduite tooa seule relation d’approbation et un échange de métadonnées unique.

Azure AD B2C des stratégies personnalisées qui utilisent hello identité expérience Framework tooenable hello tooanswer vous suivant questions :

- Quelles sont les hello juridique, la sécurité, confidentialité et les stratégies de protection de données qui doivent être respectées ?
- Quels sont les contacts hello et quels sont les processus hello pour devenir un participant agréé ?
- Qui sont hello accredited fournisseurs d’informations d’identité (également appelés « fournisseurs de revendications ») et les produits qu’ils proposent ?
- Qui sont hello accredited des parties de confiance (et éventuellement, qu’ils nécessitent-elles) ?
- Quelles sont les hello technique « sur le câble de hello » exigences d’interopérabilité pour les participants ?
- Quelles sont les règles de « exécution » opérationnel hello qui doivent être appliquées pour échanger des informations d’identité numérique ?

construction de ces questions, Azure AD B2C des stratégies personnalisées qui utilisent l’utilisation hello Framework approuver (TF) de hello identité expérience Framework tooanswer. Décrivons cette construction et ce qu’elle offre.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Comprendre la Fondation de hello Framework de confiance et de fédération de la gestion

Hello Framework de confiance est une spécification écrite de hello identité, la sécurité, confidentialité et données de stratégies de protection toowhich des participants dans une Communauté d’intérêt doivent être conforme.

L’identité fédérée fournit une base pour la protection de l’identité des utilisateurs sur Internet. En déléguant les parties de toothird de gestion des identités, une identité numérique unique pour un utilisateur final peut être réutilisée avec plusieurs parties de confiance.  

Vérification de votre identité exige que les fournisseurs d’identité (IdPs) et les fournisseurs de l’attribut (agréés) adhèrent toospecific sécurité, confidentialité et stratégies opérationnelles et pratiques.  Il ne peut effectuer des vérifications directes, parties de confiance (RPs) devez développer avec hello IdPs et agréés qu’ils choisissent toowork avec des relations d’approbation.  

Au fur et à mesure du nombre de hello des consommateurs et des fournisseurs d’informations d’identité numérique, il est difficile de toocontinue de gestion par paire de ces relations d’approbation, ou même hello exchange par paire de métadonnées technique hello qui sont requis pour la connectivité réseau .  Les hubs de fédération n’ont pas réussi à résoudre totalement ces problèmes.

### <a name="what-a-trust-framework-specification-defines"></a>Ce qui est défini par une infrastructure de confiance
TFs sont pivots du développement hello hello ouvrir identité Exchange (OIX) approbation du modèle de Framework, où chaque communauté d’intérêt est régie par une spécification de TF particulier. Ce type de spécification TF définit :

- **Hello les mesures de sécurité et confidentialité pour Communauté hello d’intérêt avec définition hello de :**
    - niveaux de Hello d’assurance (cha) qui sont proposés/requis par les participants ; par exemple, un jeu ordonné d’évaluations de confiance d’authenticité hello des informations d’identité numérique.
    - niveaux de Hello de protection (LOP) qui sont proposés/requis par les participants ; par exemple, un jeu ordonné d’évaluations de confiance pour la protection de hello numérique des informations d’identité qui sont gérées par les participants de la Communauté hello dignes d’intérêt.

- **Hello description hello numérique des informations d’identité qui a proposé/requis par les participants**.

- **stratégies techniques Hello pour la production et la consommation des informations d’identité numérique et donc de mesure cha et LOP. Ces règles sont écrites en général hello suivant des catégories de stratégies sont les suivantes :**
    - Stratégies de vérification de l’identité, par exemple : *Quel est le niveau de vérification des informations d’identité d’une personne ?*
    - Stratégies de sécurité, par exemple : *Quel est le niveau de protection de la confidentialité et de l’intégrité des informations ?*
    - Stratégies de confidentialité, par exemple : *Quel contrôle un utilisateur a-t-il sur ses informations d’identification personnelle ?*
    - Stratégies de survie, par exemple : *Si un fournisseur cesse son activité, comment fonctionne la continuité et la protection des informations d’identification personnelle ?*

- **profils de techniques Hello pour la production et la consommation des informations d’identité numérique. Ces profils incluent :**
    - Des interfaces d’étendue pour lesquelles des informations d’identité numérique sont accessibles à un niveau de garantie spécifié.
    - Des exigences techniques d’interopérabilité réseau.

- **Bonjour descriptions de hello différents rôles participants de la Communauté de hello peuvent effectuer et hello qualifications toofulfill requis à ces rôles.**

Par conséquent, une spécification de TF détermine comment les informations d’identité sont échangées entre les participants hello de communauté hello d’intérêt : parties de confiance, d’identité et fournisseurs d’attribut et vérificateurs d’attribut.

Une spécification de TF est un ou plusieurs documents servent de référence pour la gouvernance hello de communauté hello d’intérêt qui régit l’assertion de hello et de consommation des informations d’identité numérique au sein de la Communauté de hello. Il s’agit d’un ensemble documenté de stratégies et procédures conçues tooestablish de confiance dans les identités numériques hello qui sont utilisés pour les transactions entre les membres de la Communauté d’intérêt.  

En d’autres termes, une spécification de TF définit des règles de hello pour la création d’un écosystème d’identité fédérée viable pour une Communauté.

Actuellement est généralisée accord sur les avantages de hello d’une telle approche. Il est sans doute que confiance aux spécifications de framework facilitent le développement hello des écosystèmes d’identité numérique avec les caractéristiques d’assurance, de sécurité et de confidentialité vérifiables, c'est-à-dire qu’ils peuvent être réutilisés dans plusieurs communautés d’intérêt.

Pour cette raison, Azure AD B2C des stratégies personnalisées qui utilisent hello identité expérience Framework utilise la spécification de hello comme base hello de sa représentation sous forme de données pour une interopérabilité de toofacilitate TF.  

Stratégies Azure AD B2C personnalisé qui tirent parti de hello identité expérience Framework représentent une spécification de TF comme un mélange de données HWS et destinées à l’ordinateur. Certaines sections de ce modèle (en général, les sections qui sont plus adaptés pour la gouvernance) sont représentées comme référence toopublished documentation de stratégie de sécurité et de confidentialité, ainsi que de hello procédures liées (le cas échéant). Autres sections décrivent en détail hello configuration métadonnées et exécution des règles qui facilitent l’automatisation des opérations.

## <a name="understand-trust-framework-policies"></a>Présentation des stratégies d’infrastructure de confiance

En termes d’implémentation, hello spécification de TF se compose d’un ensemble de stratégies qui permettent de contrôler totalement les comportements de l’identité et les expériences.  Azure AD B2C des stratégies personnalisées qui tirent parti de hello identité expérience Framework activer vous tooauthor et créer vos propres TF via ces stratégies déclaratives qui peuvent définir et configurer :

- Hello document ou les références qui définissent l’écosystème d’identité fédérée hello de communauté hello qui lie toohello TF. Il s’agit de documentation de TF toohello des liens. Bonjour opérationnel (prédéfini) « exécution » règles ou des trajets utilisateur hello qui automatisent et/ou contrôlent exchange de hello et l’utilisation de revendications de hello. Ces parcours utilisateur sont associés à un niveau de garantie (et de protection). Une stratégie peut donc avoir des parcours utilisateur avec différents niveaux de garantie (et de protection).

- fournisseurs de revendications de fournisseurs d’identité et d’attribut Hello ou hello, dans la Communauté hello des profils de techniques qui vous intéresse et hello ils prennent en charge, ainsi que les homologation cha/LOP hello (out-of-band) qui lie toothem.

- intégration de Hello avec vérificateurs des attributs ou des fournisseurs de revendications.

- parties de confiance Hello dans la Communauté hello (par inférence).

- métadonnées Hello pour établir une communication réseau entre les participants. Ces métadonnées, ainsi que les profils techniques hello, sont utilisés pendant une transaction tooplumb « sur le format de câble hello » de l’interopérabilité entre la partie de confiance hello et les autres participants de la Communauté.

- Hello conversion de protocole, le cas échéant (par exemple, SAML, OAuth2, WS-Federation et OpenID Connect).

- conditions d’authentification Hello.

- orchestration multifacteur Hello le cas échéant.

- Un schéma partagé pour toutes les revendications hello qui sont disponibles et tooparticipants de mappages de la Communauté d’intérêt.

- Hello toutes les revendications des transformations, ainsi que de la minimisation des données hello dans ce contexte, d’exchange de hello toosustain et de l’utilisation des revendications de hello.

- liaison de Hello et le chiffrement.

- stockage de revendications Hello.

### <a name="understand-claims"></a>Présentation des revendications

> [!NOTE]
> Nous nous référons collectivement des types possibles de hello tooall des informations d’identité qui peut être échangées en tant que « revendications » : les revendications sur les informations d’identification de l’authentification d’un utilisateur final, instruction d’identité, appareil de communication, l’emplacement physique, personnelle attributs et ainsi de suite.  
>
> Nous utilisons hello terme « revendications »--plutôt que « attributs », car dans les transactions en ligne, ces artefacts de données ne sont pas faits qui peuvent être vérifiés directement par hello partie de confiance. Au lieu de cela, ils sont des assertions ou des revendications, sur des faits pour le hello de confiance doit développer les transaction demandé suffisamment confiance toogrant hello l’utilisateur final.  
>
> Nous utilisons également le terme hello « revendications » car Azure AD B2C est sont des stratégies personnalisées qui utilisent hello identité expérience Framework conçu exchange de hello toosimplify de tous les types d’informations d’identité numérique de façon cohérente, indépendamment de si hello sous-jacent protocole est défini pour la récupération de l’authentification ou un attribut utilisateur.  De même, nous utilisons le terme hello toocollectively de « fournisseurs de revendications » font référence tooidentity, fournisseurs d’attribut et les vérificateurs attribut lorsque vous ne souhaitez pas toodistinguish entre leurs fonctions spécifiques.   

Par conséquent, elles déterminent comment les informations d’identité sont échangées entre une partie de confiance, les fournisseurs d’identité et d’attributs, et les vérificateurs d’attributs. Elles spécifient les fournisseurs d’identité et d’attributs requis pour l’authentification d’une partie de confiance. Elles doivent être considérées comme un langage spécifique à un domaine, autrement dit un langage informatique spécialisé dans un domaine d’application spécifique avec de l’héritage, des instructions *if* et du polymorphisme.

Ces stratégies constituent hello lisible partie hello TF construire dans les stratégies d’Azure AD B2C personnalisé exploitant hello infrastructure expérience d’identité. Ils incluent tous les hello des détails opérationnels, y compris les métadonnées des fournisseurs de revendications et profils techniques, les définitions de schéma de revendications, les fonctions de transformation de revendications et trajets utilisateur qui sont remplis dans l’orchestration opérationnelle de toofacilitate et Automation.  

Ils sont considérés comme toobe *des documents* , car il est probable que leur contenu va évoluer concernant les participants actifs hello déclarés dans les stratégies de hello. Il existe également un risque de hello hello conditions générales pour pouvoir être un participant peut changer.  

Configuration de la fédération et de maintenance sont considérablement simplifiées par les parties de confiance reconfigurations d’approbation et de connectivité en cours de protection comme des revendications différentes fournisseurs/vérificateurs rejoindre ou quitter des (Communauté hello représentée par) hello du jeu de stratégies.

L’interopérabilité est un autre défi important. Vérificateurs/fournisseurs de revendications supplémentaires doivent être intégrés, les parties de confiance étant peu probable toosupport tous hello protocoles nécessaires. Les stratégies personnalisées Azure AD B2C résolvent ce problème en prenant en charge des protocoles standard et en appliquant des trajets d’utilisateur spécifique lors de la partie de confiance et les fournisseurs de l’attribut ne prennent pas en charge les demandes de tootranspose hello même protocole.  

Parcours de l’utilisateur incluent les profils de protocole et les métadonnées qui sont utilisé tooplumb « sur le format de câble hello » de l’interopérabilité entre la partie de confiance hello et les autres participants. Il existe également des règles de runtime opérationnelle qui sont des messages de demande/réponse tooidentity appliqué plus d’informations exchange pour appliquer la conformité avec les stratégies publiées dans le cadre de la spécification de TF hello. idée Hello de parcours de l’utilisateur est personnalisation toohello clé de l’expérience utilisateur hello. Il traite également sur le fonctionne du système de hello au niveau du protocole hello.

Sur cette base, des portails et des applications de partie de confiance peuvent, en fonction de leur contexte, appeler stratégies personnalisées que Azure AD B2C que tirer parti de hello infrastructure d’identité expérience en passant le nom hello d’une stratégie spécifique et obtenir précisément le comportement de hello et informations ils veulent sans any muss, complications ou risque de l’échange.
