---
title: "aaaMicrosoft outil de modélisation des menaces - Azure | Documents Microsoft"
description: "En savoir plus sur toutes les fonctionnalités de hello disponibles dans l’outil de modélisation des menaces de hello"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Vue d’ensemble de la fonctionnalité Outil de modélisation des menaces

Nous sommes heureux que vous avez choisi toouse hello outil de modélisation des menaces pour vos besoins de modélisation des menaces ! Si vous n’avez pas encore fait, visitez  **[prise en main de hello outil de modélisation des menaces](./azure-security-threat-modeling-tool-getting-started.md)**  notions de base toolearn hello.

> Notre outil est souvent mis à jour, reportez-vous à ce guide souvent toosee nos dernières fonctionnalités et améliorations.

En cliquant sur le bouton de « Création d’un modèle » hello ouvre une page de démarrage vierge, l’image toohello similaire ci-dessous :

![Page de démarrage vierge](./media/azure-security-threat-modeling-tool/tmtstart.png)

À l’aide du modèle des menaces hello créées par notre équipe Bonjour  **[mise en route](./azure-security-threat-modeling-tool-getting-started.md)**  exemple, nous allons nous pencher toutes les fonctionnalités de hello disponibles dans l’outil de hello aujourd'hui.

![Modèle de menaces de base](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Navigation

Avant de plonger dans les fonctionnalités intégrées hello, Attardons-nous sur hello principaux composants de hello outil

### <a name="menu-items"></a>Éléments de menu

expérience de Hello doit être d’autres produits Microsoft tooother similaires. Commençons par l’intermédiaire des éléments de menu de niveau supérieur hello :

![Éléments de menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| Étiquette                               | Détails      |
| --------------------------------------- | ------------ |
| **File** | <ul><li>Ouvrir, enregistrer et fermer des fichiers</li><li>Connexion et déconnexion aux comptes OneDrive</li><li>Partager des liens (Afficher + Modifier)</li><li>Afficher les informations sur le fichier</li><li>Appliquer le nouveau modèle tooExisting modèles</li></ul> |
| **Modifier** | Annuler/rétablir des actions, ainsi que copier, coller et supprimer |
| **Afficher** | <ul><li>Basculer entre les vues **Analyse** et **Conception**</li><li>Ouvrir des fenêtres fermées (par ex. gabarits, propriétés des éléments et messages)</li><li>Réinitialiser les paramètres de disposition toodefault</li></ul> |
| **Diagramme** | Ajouter/supprimer des diagrammes et naviguer dans les « onglets » des diagrammes |
| **Rapports** | Créer des tooshare de rapports HTML avec d’autres utilisateurs |
| **Aide** | Guide toohelp que vous utilisez l’outil de hello |

icônes de Hello sont des raccourcis pour les menus de niveau supérieur hello :

| Icône                               | Détails      |
| --------------------------------------- | ------------ |
| **Ouvrir** | Ouvre un nouveau fichier |
| **Save** | Enregistre le fichier en cours |
| **Conception** | Accède au Mode création, où vous avez créé des modèles |
| **Analyser** | Indique les menaces générées et leurs propriétés |
| **Ajouter un diagramme** | Ajoute un nouveau schéma (similaire toonew onglets dans Excel) |
| **Supprimer un diagramme** | Supprime le diagramme actuel |
| **Copier/Couper/Coller** | Copie, coupe, colle des éléments |
| **Annuler/Rétablir** | Annule/rétablit des actions |
| **Zoom avant / Zoom arrière** | Effectue un zoom et diagramme hello pour une meilleure vue |
| **Commentaires** | Ouvre hello Forum MSDN |

### <a name="canvas"></a>Canevas

espace de Hello où vous faites glisser et déposez les éléments dans. Glisser -déplacer est hello plus rapide et des modèles de toobuild de façon plus efficaces. Vous pouvez également cliquez droit et sélectionner à partir du menu hello, qui ajoute des versions génériques d’éléments hello que vous utilisez, comme indiqué ci-dessous.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Suppression du stencil de hello sur la zone de dessin hello

![Dépôt du canevas](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>En cliquant sur un gabarit de hello

![Propriétés de l’élément](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Gabarits

Où vous pouvez trouver tous les stencils toouse disponible en fonction de modèle hello sélectionné. Si vous ne pouvez pas rechercher des éléments de droite hello, essayez d’utiliser un autre modèle ou modifiez un toofit vos besoins. En règle générale, vous devez être en mesure de toofind une combinaison de catégories, telles que hello celles ci-dessous :

| Nom du gabarit                               | Détails      |
| --------------------------------------- | ------------ |
| **Processus** | Applications, plug-ins de navigateur, menaces, machines virtuelles |
| **Interacteur externe** | Fournisseurs d’authentification, navigateurs, utilisateurs, applications Web |
| **Banque de données** | Cache, stockage, fichiers de configuration, bases de données, registre |
| **Flux de données** | Binaire, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, canal nommé, DCOM/RPC, SMB, UDP |
| **Limites de bordure/ligne d’approbation** | Réseaux d’entreprise, Internet, machine, Sandbox, mode utilisateur/noyau |

### <a name="notesmessages"></a>Remarques/messages

| Composant                               | Détails      |
| --------------------------------------- | ------------ |
| **Messages** | Logique d’outil interne qui avertit les utilisateurs chaque fois qu’il existe une erreur, telle qu’aucun flux de données entre des éléments |
| **Remarques** | Notes manuelles fichier toohello ajoutés par les équipes d’ingénierie dans hello de conception et de révision |

### <a name="element-properties"></a>Propriétés de l’élément

Ceux-ci varient selon les éléments hello sélectionnés. En dehors des limites d’approbation, tous les autres éléments contiennent 3 sélections générales :

| Propriété d’élément                               | Détails      |
| --------------------------------------- | ------------ |
| **Name** | Utile pour nommer votre toobe de processus, magasins et les flux, INTERACTEURS facilement reconnu |
| **Hors de portée** | Si sélectionné, élément de hello est extraite de matrice de génération de menace hello (non recommandé) |
| **Raison de l’hors de portée** | Les utilisateurs de justification champ toolet savent pourquoi hors de portée a été sélectionnée. |

Les propriétés sont modifiées pour chaque catégorie d’élément. Cliquez sur chaque options disponibles d’élément tooinspect hello ou ouvrez toolearn de modèle hello plus. Passons maintenant les fonctionnalités hello.

## <a name="welcome-screen"></a>Écran d’accueil

écran d’accueil Hello est hello première vue lorsque vous ouvrez l’application hello.

### <a name="open-a-model"></a>Ouvrir un modèle

Passez la souris sur le bouton « Ouvrir un modèle » pour afficher 2 options masquées : « Ouvrir depuis cet ordinateur » et « Ouvrir depuis OneDrive. » Hello ouvre d’abord écran ouvrir le fichier de hello, tandis que hello ensuite vous accompagne tout processus de connexion hello pour OneDrive, autorisant les fichiers et dossiers de toopick après une authentification réussie.

![Ouvrir un modèle](./media/azure-security-threat-modeling-tool/openmodel.png)

![Ouvrir depuis l’ordinateur ou OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Commentaires, suggestions et problèmes

Cette option vous amènera toohello sur les Forums MSDN pour les outils de SDL. Il s’agit d’un toocheck excellent moyen des témoignages outil hello, y compris les solutions de contournement et de nouvelles idées sur les autres personnes.

![Commentaires](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Mode création

Chaque fois que vous ouvrez ou créez un nouveau modèle, vous serez dirigé toohello en mode Création.

### <a name="adding-elements"></a>Ajout d’éléments

Il existe 2 méthodes tooadd éléments sur la grille de hello :

- **Faites glisser et déposez** : faites glisser la grille de toohello hello élément souhaité, puis utilisez hello élément Propriétés tooprovide informations supplémentaires.
- **Bouton droit sur** : un clic droit n’importe où sur la grille de hello et sélectionnez dans la liste déroulante hello. Une représentation générique de l’élément s’affiche sur l’écran hello.

### <a name="connecting-elements"></a>Connexion des éléments

Il existe 2 méthodes tooconnect éléments dans l’outil de hello :

- **Faites glisser et déposez** : faites glisser la grille de toohello hello de flux de données souhaitée et connecter les deux extrémités toohello des éléments appropriés.
- **Cliquez sur + MAJ** : cliquez sur l’élément de premier hello (envoi de données), appuyez sur et maintenez la touche MAJ de hello, puis sélectionnez hello deuxième élément (réception de données). Cliquez avec le bouton droit, puis sélectionnez « Connecter ». Si vous utilisez un flux de données bidirectionnelle, l’ordre de hello n’est pas aussi important.

### <a name="properties"></a>Propriétés

Affiche toutes les propriétés de hello qui peuvent être modifiées sur les gabarits hello placés dans le diagramme de hello. propriétés de hello toosee, cliquez simplement sur gabarit de hello et informations de hello seront remplies en conséquence. exemple Hello ci-dessous montre avant et après un gabarit est déplacé vers le diagramme de hello « Database » :

#### <a name="before"></a>Avant

![Avant](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Après

![Après](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>Messages

Si vous créez un modèle de menace et que vous oubliez tooelements de flux de données de tooconnect, fenêtre hello du message vous informe tooact. Vous pouvez choisir tooignore ou suivez hello problème de hello toofix obtenir des instructions. 

![Messages](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Remarques

Naviguez entre les onglets de Messages tooNotes permet de vous tooadd notes tooyour diagramme toocapture toutes vos idées

## <a name="analysis-view"></a>Vue d’analyse

Une fois que vous avez terminé la création de votre diagramme basculer d’une tooanalysis vue en sélectionnant des sélections de menu du haut toohello et en choisissant la palette de peinture hello Loupe suivant toohello.

![Vue d’analyse](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Sélection de menaces générées

Lorsque vous cliquez sur une menace, vous pouvez utiliser trois fonctions uniques :

| Fonctionnalité                               | info      |
| --------------------------------------- | ------------ |
| **Indicateur de lecture** | <p>Menace est désormais marqué comme lu, ce qui peut facilement vous aider à effectuer le suivi des éléments de hello que vous avez déjà suivie</p><p>![Indicateur lu/non lu](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Focus d’interaction** | <p>L’interaction dans le diagramme hello appartenant toothat menace est mis en surbrillance.</p><p>![Focus d’interaction](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **Propriétés de la menace** | <p>Informations supplémentaires sur les menaces hello sont remplies dans la fenêtre Propriétés de menace hello</p><p>![Propriétés de la menace](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Modification de priorité

La modification du niveau de priorité hello de chaque menace généré change également leur toomake couleurs il tooidentify facilement les menaces de priorité haute, moyenne et basse.

![Modification de priorité](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Champs modifiables de propriétés de menaces

Comme indiqué dans l’image hello ci-dessus, les utilisateurs peuvent modifier les informations de hello générées par l’outil de hello une également ajouter des champs de toocertain plus d’informations, telles que la justification. Ces champs sont générés par le modèle de hello, donc si vous avez besoin de plus d’informations pour chaque menace, vous êtes invités toomake modifications.

![Propriétés de la menace](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Rapports

Une fois que vous avez terminé la modification des priorités et mise à jour hello état de chaque généré menace, vous pouvez enregistrer le fichier de hello ou imprimer un rapport en reçu trop « rapport » puis « Create rapport complet. » Vous serez invité à indiquer rapport de hello tooname, et une fois que vous le faites, vous devez voir quelque chose de similaire image toohello ci-dessous :

![Rapport](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Étapes suivantes

toocontribute un modèle pour la Communauté de hello, accédez à tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  page. **[Télécharger](https://aka.ms/tmtpreview)**  hello outil tooget dès aujourd'hui.
