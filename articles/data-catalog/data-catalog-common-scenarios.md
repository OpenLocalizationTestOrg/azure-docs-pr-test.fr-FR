---
title: "scénarios courants de catalogue de données aaaAzure | Documents Microsoft"
description: "Vue d’ensemble des scénarios courants pour Azure Data Catalog, y compris l’inscription de hello et la découverte de sources de données de valeur élevée, l’activation du décisionnel libre-service et des connaissances existantes sur des sources de données et les processus de capture."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 60930d78-d2d4-4d5d-9651-bdda50b0da0e
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: a9bd222bcf85abc31621ce7c09264a399fbb7a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-common-scenarios"></a>Scénarios courants avec Azure Data Catalog
Cet article présente des scénarios courants dans lesquels Azure Data Catalog peut aider votre organisation à mieux exploiter ses sources de données existantes.

## <a name="scenario-1-registration-of-central-data-sources"></a>Scénario 1 : Enregistrement des sources de données centrales
Les organisations ont souvent de nombreuses sources de données de grande valeur. Celles-ci incluent les systèmes d’entreprise OLTP, les entrepôts de données et les bases de données de décisionnel/analyse. Hello du nombre de systèmes et hello se chevauchent entre eux, généralement augmente au fil du temps que vos besoins et entreprise hello lui-même évolue via, par exemple, les fusions et les acquisitions.

Il peut être difficile pour l’organisation membres tooknow où toolocate hello des données au sein de ces sources de données. Questions hello suivante sont trop répandues :

* De hello HR trois systèmes utilisé au sein de l’entreprise de hello, qui faut-il utiliser toocreate ce type de rapport ?
* Où dois-je adresser tooget hello certifié les chiffres de ventes pour l’année fiscale hello que vous venez de mettre fin ?
* Qui dois-je demander ou quel est le processus de hello entrepôt de données toohello tooget accès dois-je utiliser ?
* Je ne sais pas si ces chiffres sont corrects. Qui puis-je poser pour obtenir un aperçu de la façon dont ces données sont supposées toobe utilisé avant de partager ce tableau de bord avec mon équipe ?

toothese et autres questions, Azure Data Catalog peut fournir des réponses. Hello central, valeur élevée, les sources de données de géré par informatique qui sont utilisés entre plusieurs organisations sont souvent point de départ logique hello pour le remplissage du catalogue de hello. Bien que n’importe quel utilisateur peut inscrire une source de données, dont le catalogue hello kick-started hello sources de données qui sont probablement tooprovide valeur toohello plus grand nombre d’utilisateurs permet de favoriser l’adoption et l’utilisation du système de hello. 

Si vous débutez avec Azure Data Catalog, l’identification et l’enregistrement des sources de données clés qui sont utilisées par de nombreuses équipes différentes des consommateurs de données peuvent être votre première toosuccess d’étape.

Ce scénario présente également une toomake de sources de données de valeur élevée opportunité tooannotate hello les toounderstand plus facile et l’accès. Un aspect clé de cet effort est tooinclude plus d’informations sur la façon dont les utilisateurs peuvent demander la source de données access toohello. Dans Azure Data Catalog, vous pouvez fournir l’adresse de messagerie hello de hello utilisateur ou l’équipe qui est responsable de contrôle des accès à la source de données, outils de tooexisting des liens ou documentation ou texte libre qui décrit le processus de demande d’accès hello. Ces informations vous aide à des membres qui découvrir les sources de données enregistrées, mais qui n’ont pas encore d’autorisations tooaccess hello l’accès aux données tooeasily demande à l’aide de processus hello qui sont définies et contrôlées par des propriétaires de source de données hello.

## <a name="scenario-2-self-service-business-intelligence"></a>Scénario 2 : Décisionnel libre-service
Bien que les solutions business intelligence d’entreprise traditionnelles continuer toobe paysages d’un élément important des données de nombreuses organisations, hello modification rythme de l’entreprise a apporté décisionnel libre-service plus important. Le décisionnel libre-service permet aux professionnels de l’information et aux analystes de créer leurs propres rapports, classeurs et tableaux de bord sans dépendre d’une équipe informatique centrale, et sans être limités par l’emploi du temps ou la disponibilité de l’équipe informatique.

Dans les scénarios de décisionnel libre-service, les utilisateurs combinent fréquemment des données provenant de plusieurs sources, dont un grand nombre n’ont peut-être jamais été utilisées auparavant pour le décisionnel et l’analyse. Bien que certaines de ces sources de données peuvent être déjà connues, être difficile toodiscover le toolocate toodo et évaluer les sources potentielles de données d’une tâche donnée.

En règle générale, ce processus de découverte est manuel : les analystes utilisent leur tooidentify de connexions de réseau homologue d’autres personnes qui travaillent avec des données hello recherchées. Une fois une source de données est trouvée et utilisée, hello processus se répète à nouveau pour chaque ultérieures libre-service BI d’efforts, avec plusieurs utilisateurs effectuant un processus manuel redondant de découverte.

Dans Azure Data Catalog, votre organisation peut rompre ce cycle d’efforts. Après avoir découvert une source de données classiques, un analyste peut inscrire toomake il plus facilement identifiable par d’autres utilisateurs Bonjour futures. Bien que l’analyste de hello peut ajouter plus de valeur en annotant hello inscrit les ressources de données, cette annotation n’a pas besoin tootake place à hello même moment que l’inscription. Les utilisateurs peuvent contribuer au fil du temps, en tant que leur permis de planifications, ajout progressivement les sources de données valeur toohello inscrits dans le catalogue de hello.

Cette croissance organique du contenu du catalogue hello est un complément naturel toohello fasse l’enregistrement des sources de données centrale. Catalogue de hello préalable remplissage avec des données nécessitant à de nombreux utilisateurs peut être un facteur de motivation pour la découverte et de la première utilisation. Activation des utilisateurs tooregister et annoter sources supplémentaires peuvent être un tookeep de façon les et les autres membres de l’organisation engagées.

Il est important de noter que bien que ce scénario se concentre spécifiquement sur le décisionnel libre-service, hello même défis et modèles s’appliquent à l’échelle toolarge d’entreprise des projets BI ainsi. Grâce à Data Catalog, votre organisation peut améliorer les efforts qui impliquent un processus manuel de découverte de source de données.

## <a name="scenario-3-capturing-tribal-knowledge"></a>Scénario 3 : Capture des connaissances tribales
Comment savoir quelles données vous devez toodo votre travail et où toofind ces données ?

Si vous occupez le même poste depuis un certain temps, vous connaissez probablement la réponse. Vous aurez parcouru de progressive processus d’apprentissage et au fil du temps avez permis de découvrir les sources de données hello qui sont des clés tooyour au quotidien.

Lorsqu’un nouvel employé rejoint votre équipe, en quoi cette personne savoir quelles données sont requises pour le travail de hello et où toofind il ?

Il est fort probable nouvelle personne de hello est fourni tooyou avec ces questions.

Ce transfert en cours de connaissances en termes fait partie du processus de détection de source de données hello dans les petites et grandes organisations. Membres d’équipe plus hauts et expérimentés ont émergé connaissances années hello et membres plus récente de l’équipe ont permis de tooask lorsque vous avez des questions. fréquence à laquelle les informations critiques Hello existent uniquement dans les têtes hello de quelques personnes, et lorsque les utilisateurs sont en vacances ou laisser l’équipe de hello, organisation de hello sont affectées.

Données experts normalement effectuer un toodocument effort leurs connaissances, il partage par courrier électronique ou dans des documents Word sur un site d’équipe SharePoint. Bien que cette approche peut être utile, elle introduit un nouveau problème de détection : comment les personnes savoir quels documents existe et où toofind il ?

Avec Azure Data Catalog, votre organisation dispose d’un emplacement unique et centralisé pour le stockage et le partage de ces connaissances tribales, et pour leur mise à disposition sans difficulté. Dans le catalogue de données, les experts de vos données peuvent annoter directement des ressources de données et fournissent des liens tooexisting documentation. Lorsque les membres de l’organisation utilisent hello catalogue toodiscover une source de données, ils trouverez non seulement les source hello lui-même, mais également les connaissances hello qui existaient précédemment uniquement dans les esprits hello d’experts de votre organisation.
