---
title: "aaaGetting démarré - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "Il s’agit d’une vue d’ensemble plus approfondis hello outil de modélisation de menace dans l’action de mise en surbrillance."
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
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Prise en main de hello outil de modélisation des menaces

Hello Cloud et les outils de sécurité d’entreprise de l’équipe a publié hello aperçu d’outil de modélisation des menaces cette année comme étant un libre  **[-cliquez pour télécharger](https://aka.ms/tmtpreview)**. modification Hello dans le mécanisme de remise nous permet des toocustomers de hello de toopush plus récente d’améliorations et correctifs de bogues chaque fois qu’ils ouvrent outil hello, qui facilitent toomaintain et utilisation.
Cet article vous guide tout au long des processus de hello de mise en route avec l’approche de modélisation des menaces SDL Microsoft hello et vous montre comment toouse hello outil toodevelop grande menace pour la modèles comme structure fondamentale de votre processus de sécurité.

Cet article s’appuie sur les connaissances existantes de l’approche de modélisation des menaces SDL hello. Pour un examen rapide, consultez trop**[menace pour la modélisation des Applications Web](https://msdn.microsoft.com/library/ms978516.aspx)**  et une version archivée du  **[défauts sécurité découvrir à l’aide de hello méthode STRIDE](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  Article MSDN publié en 2006.

tooquickly résumer, l’approche de hello implique la création d’un diagramme, identification des menaces, les corriger et validation de chaque atténuation. Voici un diagramme qui met en évidence ce processus :

![Traitement SDL](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Démarrage du processus de modélisation des menaces hello

Lorsque vous lancez hello outil de modélisation des menaces, vous remarquerez quelques éléments, comme indiqué dans l’image de hello :

![Page de démarrage vierge](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>Section de modèle des menaces

| Composant                                   | Détails                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Bouton de commentaires, suggestions et problèmes** | Prend vous hello  **[Forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  pour tous les éléments SDL. Il vous donne un tooread opportunité à ce que les autres utilisateurs font, ainsi que les solutions de contournement et des recommandations. Si vous ne trouvez toujours ce que vous cherchez, envoyez un e-mail tmtextsupport@microsoft.com pour notre toohelp équipe de support vous                                                                                                                            |
| **Créer un modèle**                          | Ouvre un canevas vierge pour vous toodraw votre diagramme. Assurez-vous que tooselect quel est le modèle vous aimeriez toouse pour votre modèle                                                                                                                                                                                                                                                                                                                                                                       |
| **Modèle pour de nouveaux modèles**                 | Vous devez sélectionner le toouse modèle avant de créer un modèle. Notre modèle principal est hello Azure menace de modèle, qui contient les gabarits, les menaces et les solutions d’atténuation Azure spécifique. Pour les modèles génériques, sélectionnez hello SDL TM de connaissances à partir du menu déroulant de hello. Que toocreate votre propre modèle, ou soumettre une pour tous les utilisateurs ? Découvrez notre  **[modèle référentiel](https://github.com/Microsoft/threat-modeling-templates)**  toolearn GitHub Page plus                              |
| **Ouvrir un modèle**                            | <p>Ouvre des modèles de menaces précédemment enregistrés. fonctionnalité d’ouvrir les modèles récemment Hello est élevée si vous avez besoin de tooopen vos fichiers les plus récents. Lorsque vous pointez sur la sélection de hello, vous trouverez 2 méthodes tooopen modèles :</p><p><ul><li>Ouvrir depuis cet ordinateur : un moyen classique d’ouvrir un fichier à l’aide du stockage local</li><li>Ouvrir à partir de OneDrive – les équipes peuvent utiliser des dossiers dans OneDrive toosave et le partager leurs modèles de menace dans un emplacement unique toohelp augmentation de la productivité et de collaboration</li></ul></p> |
| **Guide de démarrage**                   | Ouvre hello  **[outil de modélisation de menace Microsoft](./azure-security-threat-modeling-tool.md)**  page principale                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>Section de modèle

| Composant               | Détails                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Créer un nouveau modèle** | Ouvre un modèle vierge pour vous toobuild sur. À moins d’avoir une connaissance approfondie de la création de modèles à partir de rien, nous vous recommandons toobuild parmi ceux qui sont existant |
| **Ouvrir un modèle**       | Ouvre les modèles existants pour vous toomake modifications trop                                                                                                             |

équipe d’outil de modélisation des menaces Hello fonctionne en permanence expérience et la fonctionnalité de l’outil tooimprove. Quelques modifications mineures peuvent avoir lieu pendant l’année de hello hello, mais toutes les modifications majeures nécessitent réécritures dans le guide de hello. Consultez tooit souvent les tooensure vous obtenez les dernières annonces de hello.

## <a name="building-a-model"></a>Création d’un modèle

Dans cette section, nous parlons de :

- Cristina (un développeur)
- Ricardo (un responsable des programmes) et
- Ashish (un testeur)

Ils sont en cours sur le processus hello du développement de leur premier modèle des menaces.

> Ricardo : Bonjour Cristina, j’ai travaillé sur un diagramme de modèle de menace hello et souhaitiez toomake que nous a obtenu les détails hello droite. Pouvez-vous m’aider à vérifier ?
> Cristina : absolument. Jetons un œil sur cette configuration.
> Ricardo ouvre hello outil et porte le même son écran Cristina.

![Modèle de menaces de base](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina : Ok, ça semble simple, mais pouvez-vous m’aider ?
> Ricardo : Bien sûr ! Voici la répartition de hello :
> - Notre utilisateur humain est dessiné comme une entité extérieure, un carré
> - Ils vous envoyez le serveur Web de tooour commandes : cercle de hello
> - serveur Web de Hello est consultant une base de données (deux lignes parallèles)

Ce que Ricardo vient de montrer à Cristina est un DFD, abréviation de **[diagramme de flux de données](https://en.wikipedia.org/wiki/Data_flow_diagram)**. Hello, outil de modélisation des menaces permet des limites d’approbation aux utilisateurs toospecify, indiqués en pointillés rouge de hello, tooshow où différentes entités se trouvent dans le contrôle. Par exemple, les administrateurs informatiques requièrent un système Active Directory à des fins d’authentification, hello Active Directory est en dehors de leur contrôle.

> Cristina : Recherche toome droite. Que se passe-t-il pour les menaces de hello ?
> Ricardo : je vais vous montrer.

## <a name="analyzing-threats"></a>Analyse des menaces

Une fois qu’il clique sur la vue d’analyse hello de hello icône sélection du menu (fichier Loupe), il provient d’une liste de tooa des menaces généré hello outil de modélisation des menaces trouvées en fonction de modèle par défaut de hello, qui utilise l’approche SDL hello appelée  **[ STRIDE (usurpation d’identité, falsification, la divulgation d’informations, déni de Service et élévation de privilèges)](https://en.wikipedia.org/wiki/STRIDE_(security))**. idée de Hello est que le logiciel provient sous un jeu prévisible des menaces, ce qui se trouve à l’aide de ces 6 catégories.

Cette approche est que la sécurisation de votre maison en s’assurant que chaque porte et fenêtre a un mécanisme de verrouillage en place avant d’ajouter un système d’alarme ou de repérage après voleur de hello.

![Menaces de base](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo commence en sélectionnant hello premier élément de liste de hello. Voici ce qui se passe :

Tout d’abord, interaction hello entre deux gabarits de hello est améliorée

![Interaction](./media/azure-security-threat-modeling-tool/interaction.png)

Deuxième, d’autres informations sur les menaces hello s’affiche dans la fenêtre de propriétés de la menace hello

![Informations d’interaction](./media/azure-security-threat-modeling-tool/interactioninfo.png)

menace de Hello généré lui permet de comprendre les défauts de conception potentiels. catégorisation de STRIDE Hello lui donne une idée sur des vecteurs d’attaque potentielle, hello lors de la description supplémentaire lui indique exactement ce qui est incorrect, ainsi que d’éventuels moyens toomitigate il. Il peut utiliser des notes de toowrite champs modifiables dans les détails de la justification hello ou modification des classements de priorité en fonction de la barre de bogue de son organisation.

Modèles Azure ont les utilisateurs de toohelp des détails supplémentaires de comprendre non seulement ce qui est incorrect, mais aussi comment toofix il en ajoutant des liens hypertexte, des exemples et des descriptions de documentation de tooAzure spécifique.

description de Hello augmentait à réaliser l’importance de hello d’ajout d’un utilisateur tooprevent du mécanisme d’authentification à partir de l’usurpation, révélant hello première menace toobe travaillé sur. Quelques minutes dans la discussion hello avec Cristina, ils compris importance hello de l’implémentation du contrôle d’accès et de rôles. Ricardo renseigné certains toomake remarques qu’ils ont été implémentés.

Comme Ricardo a été introduite dans menaces hello sous la divulgation d’informations, il cadre du plan de contrôle d’accès hello requis certains comptes en lecture seule pour la génération de rapport et d’audit. Il a demandé si ce doit être une nouvelle menace, mais hello atténuation ont été hello, donc il noter les menaces hello en conséquence.
Il également pensé, à la divulgation d’informations, un peu plus et réalisé que les bandes de sauvegarde hello se tooneed le chiffrement, un travail de l’équipe des opérations hello.

Menaces conception toohello non applicable en raison de la sécurité ou les solutions d’atténuation tooexisting garantit peut être modifié trop « Non Applicable » à partir de hello état de liste déroulante. Il existe trois autres possibilités : n’a pas démarré : sélection par défaut, Needs Investigation – utilisé toofollow sur les éléments et atténué – une fois qu’elle est entièrement travaillé sur.

## <a name="reports--sharing"></a>Rapports et partage

Ricardo parcourt la liste hello avec Cristina et ajoute les remarques importantes, les solutions d’atténuation/justification, priorité et l’état change, he sélectionne Rapports -> Création de rapports complète -> Enregistrer le rapport, qui imprime une jolie de rapports lui toogo via avec travail de sécurité appropriées collègues tooensure hello est implémentée.

![Informations d’interaction](./media/azure-security-threat-modeling-tool/report.png)

Si Ricardo veut fichier hello de tooshare au lieu de cela, il peut facilement faire, l’enregistrement dans le compte de OneDrive de son organisation. Une fois qu’il le fait, il peut copier le lien de document hello et partagez-le avec ses collègues. 

## <a name="threat-modeling-meetings"></a>Réunion sur la modélisation des menaces

Lorsque les Ricardo envoyées son collègue toohis de modèle de menace à l’aide de OneDrive, Ashish, testeur de hello, a été underwhelmed. Il semblait que Ricardo et Cristina avaient manqué quelques cas particuliers importants, qui pouvaient être facilement compromis. Son scepticisme est modèles de toothreat de complément.

Dans ce scénario, après Ashish nécessaire sur le modèle de menace hello, il appelée pour les deux réunions de modélisation de menace : toosynchronize une réunion sur le processus de hello et parcourez les diagrammes de hello, puis une deuxième réunion de révision de la menace et de déconnexion.

Dans la première réunion de hello, Ashish passé à tout le monde via le processus de modélisation des menaces SDL hello parcourant les 10 minutes. Puis, il a activé le diagramme de modèle de menace hello et démarré il explique en détail. Au bout de cinq minutes, un important composant manquant a été identifié.

Quelques minutes par la suite, Ashish et Ricardo obtenu dans une présentation détaillée de la façon dont le serveur de Web hello a été créé. Il n’était pas hello permet un tooproceed réunion, mais chacun d’eux par la suite que découverte écart de hello tôt allait toosave que les temps hello futures.

Bonjour deuxième réunion, équipe hello passé en revue les menaces hello, décrit certaines tooaddress façons les et signés désactivée sur le modèle des menaces hello. Ils archivées de document de hello dans le contrôle de code source et de suite avec le développement.

## <a name="thinking-about-assets"></a>Réfléchir sur les ressources

Certains lecteurs dont les menaces sont modélisées peuvent remarquer que nous n’avons pas du tout parlé des ressources. Nous avons découvert que de nombreux ingénieurs logiciels comprennent mieux qu’ils comprennent le concept de hello de ressources et des ressources, un intrus peut être intéressé par leurs logiciels.

Si vous souhaitez toothreat du modèle d’une maison, vous pouvez commencer par réfléchir à votre familles, irremplaçables photos ou précieux. Par exemple, vous pouvez commencer par réfléchir à qui peuvent interrompre les et le système de sécurité actuel hello. Ou bien, vous pouvez commencer en prenant en considération hello caractéristiques physiques, telles que le pool de hello ou véranda hello. Il s’agit toothinking analogue sur les ressources, des personnes malveillantes ou de conception de logiciels. Ces trois approches fonctionnent.

modélisation de toothreat Hello approche que nous avons présenté ici est considérablement plus simple que Microsoft a consisté Bonjour passées. Nous avons constaté que l’approche de conception de logiciel hello fonctionne bien pour de nombreuses équipes. Nous espérons inclure la vôtre.

## <a name="next-steps"></a>Étapes suivantes

Envoyez vos questions, commentaires et vos préoccupations tootmtextsupport@microsoft.com. **[Télécharger](https://aka.ms/tmtpreview)**  tooget d’outil de modélisation des menaces hello a démarré.
