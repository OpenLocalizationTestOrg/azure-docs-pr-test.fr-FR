---
title: "historique des versions d’aaaConnector | Documents Microsoft"
description: "Cette rubrique répertorie toutes les versions de connecteurs de hello pour Forefront Identity Manager (FIM) et Microsoft Identity Manager (MIM)"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>Historique de publication des versions du connecteur
Connecteurs Hello pour Forefront Identity Manager (FIM) et Microsoft Identity Manager (MIM) sont fréquemment mis à jour.

> [!NOTE]
> Cette rubrique ne concerne que FIM et MIM. Ces connecteurs ne sont pas pris en charge pour l’installation sur Azure AD Connect. Connecteurs finales sont préinstallés sur AADConnect toospecified Build de la mise à niveau.

Cette rubrique répertorie toutes les versions de hello connecteurs qui ont été publiées.

Liens connexes :

* [Télécharger les derniers connecteurs](http://go.microsoft.com/fwlink/?LinkId=717495)
* [connecteur LDAP générique](active-directory-aadconnectsync-connector-genericldap.md)
* [connecteur SQL générique](active-directory-aadconnectsync-connector-genericsql.md)
* [connecteur WebServices](http://go.microsoft.com/fwlink/?LinkID=226245)
* [connecteur PowerShell](active-directory-aadconnectsync-connector-powershell.md)
* [connecteur Lotus Domino](active-directory-aadconnectsync-connector-domino.md)


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (AADConnect en attente de publication)


### <a name="fixed-issues"></a>Problèmes résolus :

* Services web génériques :
  * Correction d’un problème empêchant la création d’un projet SOAP lorsqu’il existait deux points de terminaison ou plus.
* SQL générique :
  * Dans l’opération d’importation de hello hello GSQL a été pas conversion de l’heure correctement, quand enregistré tooconnector espace. format de date et d’heure par défaut pour l’espace de connecteur de hello GSQL Hello a été remplacé par 'AAAA-MM-JJ : ssZ' too'yyyy-MM-JJ : ssZ '.

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Problèmes résolus :

* Services web génériques :
  * outil de Wsconfig Hello ne n’a pas converti correctement tableau Json de hello à partir de « exemple de demande » pour la méthode de service REST hello. Cela a provoqué des problèmes avec la sérialisation ce tableau Json pour la demande REST hello.
  * L’outil de configuration du connecteur de service web ne prend pas en charge l’utilisation de symboles d’espace dans les noms d’attribut JSON 
    * Un modèle de Substitution peut être ajouté manuellement toohello WSConfigTool.exe.config fichier, par exemple```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes :
  * Lorsque hello option **autoriser certificateurs personnalisés pour les unités d’organisation/organisation** est désactivée puis échoue de connecteur hello lors de l’exportation (mise à jour) après l’exportation de hello transmet tous les attributs est exportée tooDomino mais au moment de hello de exportation KeyNotFoundException est retournée tooSync. 
    * Cela se produit car hello renommer échoue lorsqu’il tente toochange DN (attribut de nom d’utilisateur) en modifiant un des attributs hello ci-dessous :  
      - LastName
      - FirstName
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - Unité d’organisation
      - altcommonname

  * Quand l’option **Allow custom certifiers for Organization/Organizational Units** (Autoriser les certificateurs personnalisés pour les organisations/unités d’organisation) est activée, mais que les certificateurs nécessaires sont encore vides, une exception KeyNotFoundException se produit.

### <a name="enhancements"></a>Améliorations :

* SQL générique :
  * **Scénario : repensé Implémenté  : fonctionnalité**  « * »
  * **Description de la solution :** modification de l’approche pour la [gestion des attributs de référence à valeurs multiples](active-directory-aadconnectsync-connector-genericsql.md).


### <a name="fixed-issues"></a>Problèmes résolus :

* Services web génériques :
  * Impossible d’importer la configuration serveur si le connecteur de service web est présent
  * Le connecteur de service web ne fonctionne pas avec plusieurs services web

* SQL générique :
  * Aucun type d’objet n’est répertorié pour l’attribut référencé à valeur unique
  * L’importation différentielle sur la stratégie Change Tracking supprime objet lorsque la valeur est supprimée de la table à valeurs multiples
  * OverflowException dans le connecteur GSQL avec DB2 sur AS/400

Lotus :
  * Tooenable\disable d’ajout de l’option recherche des unités d’organisation avant d’ouvrir la page de GlobalParameters

## <a name="114430"></a>1.1.443.0

Publié : mars 2017

### <a name="enhancements"></a>Améliorations

* SQL générique :</br>
  **Scénario symptômes :** il s’agit d’une limitation connue de hello connecteur SQL où nous uniquement un type référence d’objet tooone et obligent référence croisée avec des membres. </br>
  **Description de la solution :** à l’étape de traitement hello pour les références ont été « * » option est sélectionnée, toutes les combinaisons de types d’objet seront affichera comme moteur de synchronisation toohello précédent.

>[!Important]
- Cela crée de nombreux espaces réservés.
- Il est requis toomake que hello d’affectation de noms est unique entre les types d’objets.


* LDAP générique :</br>
 **Scénario :** lorsque que certains conteneurs sont sélectionnées dans une partition spécifique, puis recherche de hello toujours s’effectue dans une partition entière. La partition spécifique est filtrée par le service de synchronisation et non par MA, ce qui peut entraîner une dégradation des performances. </br>

 **Description de la solution :** toomake de code du connecteur GLDAP de modifié il est possible de passer par tous les conteneurs et rechercher des objets dans chacune d’elles, au lieu de rechercher dans la partition de toute hello.


* Lotus Domino :

  **Scénario :** Prise en charge de la suppression d’un courrier Domino pour la suppression d’une personne pendant une exportation. </br>
  **Solution :** Prise en charge de la suppression d’un courrier configurable pour la suppression d’une personne pendant une exportation.

### <a name="fixed-issues"></a>Problèmes résolus :
* Services web génériques :
 * Lors de la modification par défaut des URL du service hello SAP wsconfig projets via l’outil de Configuration de service Web puis hello l’erreur suivante se produit : Impossible de trouver une partie du chemin d’accès de hello

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* LDAP générique :
 * Le connecteur GLDAP ne voit pas tous les attributs dans AD LDS
 * Assistant sauts lorsqu’aucun attribut UPN n’est détectées dans le schéma d’annuaire LDAP hello
 * Les échecs d’importation delta avec erreurs de détection n’apparaissent pas pendant l’importation complète, lorsque l’attribut « objectclass » n’est pas sélectionné.
 * Une page de configuration « Configurer des Partitions et des hiérarchies », n’affiche pas tous les objets que le type est partition toohello égal pour les nouveaux serveurs Bonjour générique  
générique. Seuls les objets de la partition RootDSE sont affichés.


* SQL générique :
 * Correction du bogue empêchant l’importation d’un attribut à valeurs multiples d’importation delta de filigrane SQL générique
 * Lors de l’exportation des valeurs supprimées\ajoutées d’un attribut à valeurs multiples, celles-ci ne sont pas supprimées\ajoutées dans la source de données.  


* Lotus Notes :
 * Un champ « Nom complet » est indiqué dans le métaverse de hello correctement toutefois lors de l’exportation tooNotes hello valeur pour les attributs hello est Null ou vide.
 * Correction d’erreur de certification en double
 * Lors de hello objet sans aucune donnée est sélectionnée sur hello connecteur pour Lotus Domino avec d’autres objets puis nous erreur hello découverte lors de l’importation complète.
 * Lors de l’importation de Delta est en cours d’exécution sur hello connecteur Lotus Domino à fin hello de cette exécution, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service parfois renvoie une erreur d’Application.
 * L’appartenance au groupe global fonctionne correctement et est conservée, sauf lors de l’exécution hello exportation tootry tooremove un utilisateur d’appartenance, il montre aussi efficace avec une mise à jour, utilisateur de hello réellement ne sont supprimé de l’appartenance à Lotus Notes.
 * Un mode de toochoose opportunité d’exportation en tant que « Ajouter l’élément bas » a été ajouté dans la configuration de l’interface graphique utilisateur de Lotus MA tooappend de nouveaux éléments en bas lors de l’exportation de hello pour les attributs à valeurs multiples.
 * Connecteur ajoutera hello nécessaire fichier hello logique toodelete hello dossier courrier et ID de coffre.
 * La suppression d’appartenance ne fonctionne pas pour un membre NAB croisé.
 * Les valeurs devraient être supprimées correctement de l’attribut à valeurs multiples.

## <a name="111170"></a>1.1.117.0
Publié : mars 2016

**Nouveau connecteur**  
Version de hello initiale [générique connecteur SQL](active-directory-aadconnectsync-connector-genericsql.md).

**Nouvelles fonctionnalités :**

* Connecteur LDAP générique :
  * Prise en charge supplémentaire pour l’importation delta avec Isode.
* Connecteur des services web :
  * Hello mis à jour csEntryChangeResult activité et setImportErrorCode activité tooallow objet erreurs de niveau toobe toohello arrière retourné moteur de synchronisation.
  * Hello mis à jour SAP6 et SAP6User modèles toouse hello nouvel objet erreur au niveau des fonctionnalités.
* Connecteur Lotus Domino :
  * Lors de l’exportation, vous avez besoin d’une autorité de certification par carnet d’adresses. Vous pouvez maintenant utiliser hello même mot de passe pour toute certificateurs toomake hello la gestion plus facile.

**Problèmes résolus :**

* Connecteur LDAP générique :
  * Pour IBM Tivoli DS, certains attributs de référence n’étaient pas été détectés correctement.
  * Pour LDAP ouvert pendant une importation delta, les espaces blancs au début de hello et la fin de chaînes a été tronqués.
  * Pour Novell et NetIQ, une exportation qui déplacer un objet entre les unités d’organisation/conteneurs et à hello même moment l’objet renommé hello a échoué.
* Connecteur des services web :
  * Si le service web de hello a plusieurs points de terminaison pour la même liaison, puis hello connecteur n’a pas correctement détecté ces points de terminaison.
* Connecteur Lotus Domino :
  * Une exportation de hello fullName attribut tooa messagerie de base de données n’a pas fonctionné.
  * Une exportation quel membre ajouté et supprimé à partir d’un groupe uniquement exportée hello membres ont été ajoutés.
  * Si un Document de notes de publication n’est pas valide (hello attribut isValid défini toofalse), puis hello échoue de connecteur.

## <a name="older-releases"></a>Versions plus anciennes
Avant mars 2016, hello connecteurs ont été publiés dans les rubriques de prise en charge.

**LDAP générique**

* [KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, septembre 2015
* [KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, mars 2015
* [KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, janvier 2015
* [KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, septembre 2014
* [KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, mars 2014

**WebServices**

* [KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, septembre 2014

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, septembre 2014

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, septembre 2015
* [KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, mars 2015
* [KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, août 2014
* [KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, février 2014  
* [KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, octobre 2013
* [KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, août 2013

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
