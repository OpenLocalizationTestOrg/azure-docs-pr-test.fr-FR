---
title: "sécurité au niveau aaaRow avec Power BI Embedded"
description: "Détails sur la sécurité au niveau des lignes avec Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Sécurité au niveau des lignes avec Power BI Embedded

Sécurité au niveau des lignes (RLS) peut être utilisé toorestrict utilisateur accès tooparticular données dans un rapport ou un jeu de données, permettant de plusieurs utilisateurs différents toouse hello même rapport lors de voir toutes les données de différents. Power BI Embedded prend désormais en charge les jeux de données configurés avec la fonction RLS.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

Dans parti tootake de commande de la sécurité RLS, il est important de que comprendre les trois concepts principaux ; Les utilisateurs, rôles et des règles. Examinons-les de plus près :

**Les utilisateurs** : ces utilisateurs finaux réelle de hello les rapports sont affichés. Dans Power BI Embedded, les utilisateurs sont identifiés par la propriété de nom d’utilisateur hello dans un jeton d’application.

**Rôles** – les utilisateurs appartiennent tooroles. Un rôle fait office de conteneur pour les règles et peut avoir pour nom « Directeur des ventes » ou « Représentant ». Dans Power BI Embedded, les utilisateurs sont identifiés par la propriété de rôles hello dans un jeton d’application.

**Règles** : rôles ont des règles, et ces règles sont les filtres réel hello qui vont toobe appliqué toohello données. Cela peut être aussi simple que « Pays = États-Unis » ou bien quelque chose de plus dynamique.

### <a name="example"></a>Exemple

Pour le reste de hello de cet article, nous vous fournirons un exemple de création de lignes et qui consomme ensuite au sein d’une application embedded. Notre exemple utilise hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) fichier PBIX.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Notre exemple analyse de vente au détail affiche les ventes pour tous les magasins hello dans une chaîne de vente au détail spécifique. Sans RLS, quel que soit le secteur manager se connecte et vues hello des rapports, il voit hello des mêmes données. Direction a déterminé que chaque directeur de district doit voir uniquement hello ventes des magasins hello qu’elles gèrent, toodo cela, nous pouvons utiliser des lignes.

RLS est créé dans Power BI Desktop. Lors de l’ouverture hello dataset et le rapport, nous pouvons basculer toodiagram afficher le schéma hello toosee :

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Voici quelques éléments toonotice, avec ce schéma :

* Toutes les mesures, telles que **Total des ventes**, sont stockés dans hello **Sales** table de faits.
* Il existe quatre tables de dimension connexes supplémentaires : **Item**, **Time**, **Store** et **District**.
* Hello sur les lignes de relation hello indiquent la manière dont les filtres peuvent être transmis à partir d’une table tooanother. Par exemple, si un filtre est placé sur **heure [Date]**, dans le schéma actuel de hello elle permet uniquement de filtrer les valeurs Bonjour **Sales** table. Aucune autre table ne serait affectés par ce filtre toutes les flèches hello sur la table ventes du point toohello lignes relation hello et pas immédiatement.
* Hello **District** table indique qui est responsable de hello pour chaque zone géographique :
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

En fonction de ce schéma, si nous appliquons un filtre toohello **directeur de District** colonne hello table du secteur, et si ce filtre correspond à l’utilisateur hello affichage rapport de hello, que le filtre sera également filtrer vers le bas hello **magasin**et **Sales** tables tooonly affichent des données pour ce secteur particulier manager.

Voici comment procéder :

1. Sous l’onglet de modélisation hello, cliquez sur **gérer les rôles**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Créer un rôle nommé **Directeur**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. Bonjour **District** table entrez hello DAX expression suivante : **[directeur de District] = USERNAME()**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. les règles hello que toomake travaillez sur hello **modélisation** , cliquez sur **afficher comme rôles**et puis entrez hello qui suit :  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Hello rapports maintenant affichent les données comme si vous étiez connecté en tant que **Andrew Ma**.

L’application hello filtre, méthode hello nous l’avons fait ici, filtre vers le bas tous les enregistrements de hello **District**, **magasin**, et **Sales** tables. Toutefois, en raison de la direction du filtrage hello sur les relations hello entre **Sales** et **temps**, **Sales** et **élément**et **Élément** et **temps** tables ne sont pas filtrés vers le bas.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Qui peut être OK de cette exigence, cependant, si nous ne voulons pas gestionnaires toosee les éléments pour lesquels ils n’ont pas de ventes, nous pouvons activer bidirectionnel le filtrage croisé pour hello relation et flux hello filtre de sécurité dans les deux sens. Cela est possible en modifiant la relation hello entre **Sales** et **élément**, comme suit :

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Désormais, les filtres peuvent également se dérouler à partir de hello Sales table toohello **élément** table :

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Si vous utilisez le mode DirectQuery pour vos données, vous devez tooenable bidirectionnel cross filtrage en sélectionnant ces deux options :

1. **Fichier** -> **Options et paramètres** -> **Fonctionnalités en préversion** -> **Activer le filtrage croisé dans les deux directions pour DirectQuery**.
2. **Fichier** -> **Options et paramètres** -> **DirectQuery** -> **Autoriser la mesure sans restriction en mode DirectQuery**.

toolearn plus d’informations sur le filtrage croisé bidirectionnel, téléchargement hello [filtrage croisé bidirectionnel dans SQL Server Analysis Services 2016 et Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) livre blanc.

Ceci conclut tout le travail hello doit toobe effectué dans Power BI Desktop, mais il existe un plus d’élément de travail qui doit toobe fait toomake hello RLS règles que nous avons défini le travail dans Power BI Embedded. Les utilisateurs sont authentifiés et autorisés par votre application et les jetons de l’application sont toogrant utilisé ce tooa spécifique Power BI Embedded rapport d’accès utilisateur. Power BI Embedded ne dispose pas d’informations spécifiques relatives à l’utilisateur. Pour la sécurité RLS toowork, vous aurez besoin de toopass un contexte supplémentaire dans le cadre de votre jeton d’application :

* **nom d’utilisateur** (facultatif) : utilisé avec la sécurité RLS Ceci est une chaîne qui peut être utilisée toohelp identifier l’utilisateur de hello lors de l’application des règles RLS. Voir Utilisation de la sécurité au niveau des lignes avec Power BI Embedded
* **rôles** : une chaîne contenant hello rôles tooselect lors de l’application des règles de sécurité de niveau ligne. Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes.

Vous créez un jeton de hello à l’aide de hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) (méthode). Si la propriété de nom d’utilisateur hello est présente, vous devez également passer au moins une valeur dans les rôles.

Par exemple, vous pouvez modifier hello EmbedSample. La ligne 55 de DashboardController peut être changée, de

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

to

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

jeton d’application complet Hello ressemble à ceci :

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Désormais, avec toutes les parties hello ensemble, lorsqu’un utilisateur connecte à notre tooview application ce rapport, ils uniquement serez qu’ils sont autorisés à toosee, les données de salutation toosee en mesure de tel que défini par la sécurité au niveau des lignes.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Voir aussi

[Sécurité au niveau des lignes (RLS) avec Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)

