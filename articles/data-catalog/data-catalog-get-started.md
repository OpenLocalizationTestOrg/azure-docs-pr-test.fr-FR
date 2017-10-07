---
title: "aaaGet a démarré avec le catalogue de données | Documents Microsoft"
description: "Didacticiel de bout en bout présentant les scénarios hello et les fonctionnalités d’Azure Data Catalog."
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Prise en main d’Azure Data Catalog
Azure Data Catalog est un service cloud entièrement géré qui sert de système d’inscription et de découverte des ressources de données d’entreprise. Pour une présentation détaillée, consultez l’article [Qu’est-ce qu’Azure Data Catalog ?](data-catalog-what-is-data-catalog.md).

Ce didacticiel vous permet de commencer à utiliser Azure Data Catalog. Vous effectuez hello suivant les procédures décrites dans ce didacticiel :

| Procédure | Description |
|:--- |:--- |
| [Approvisionner Data Catalog](#provision-data-catalog) |Dans cette procédure, vous créez ou configurez Azure Data Catalog. Vous effectuez cette étape uniquement si le catalogue de hello n’a pas été définie avant. Vous ne pouvez avoir qu’un seul catalogue de données par organisation (domaine Microsoft Azure Active Directory), même si plusieurs abonnements sont associés à votre compte Azure. |
| [Inscrire des ressources de données](#register-data-assets) |Dans cette procédure, vous inscrivez des ressources de données à partir de la base de données exemple hello AdventureWorks2014 avec le catalogue de données hello. Inscription consiste hello extraction métadonnées structurelles clées telles que les noms, les types et les emplacements à partir de la source de données hello et la copie de ce catalogue toohello de métadonnées. Hello source de données et de vos données restent où ils sont, mais les métadonnées de hello sont utilisées par hello catalogue toomake les plus facilement identifiables et plus compréhensible. |
| [Découvrir les ressources de données](#discover-data-assets) |Dans cette procédure, vous utilisez hello Azure Data Catalog toodiscover portail données actifs qui ont été enregistrés à l’étape précédente de hello. Après l’inscription d’une source de données avec Azure Data Catalog, ses métadonnées sont indexée par le service de hello afin que les utilisateurs peuvent rechercher facilement des données hello que dont ils ont besoin. |
| [Annoter les ressources de données](#annotate-data-assets) |Dans cette procédure, vous fournissez des annotations (informations telles que les descriptions, les balises, la documentation ou experts) hello pour les ressources de données. Ces informations complètent les métadonnées hello extraites à partir de la source de données hello et d’autres personnes toomore compréhensible de source de données de hello toomake. |
| [Se connecter toodata actifs](#connect-to-data-assets) |Dans cette procédure, vous ouvrez les ressources de données dans des outils clients intégrés (comme Excel et SQL Server Data Tools) et dans un outil non intégré (SQL Server Management Studio). |
| [Gérer les ressources de données](#manage-data-assets) |Dans cette procédure, vous configurez la sécurité de vos ressources de données. Catalogue de données ne donne pas les utilisateurs accéder aux données de toohello lui-même. propriétaire Hello hello de source de données contrôle l’accès aux données. <br/><br/> Avec le catalogue de données, vous pouvez découvrir des sources de données et hello de vue **métadonnées** liés sources toohello inscrits dans le catalogue de hello. Il peut arriver, toutefois, dans lequel les sources de données doivent être visible toospecific seuls utilisateurs ou toomembers de groupes spécifiques. Pour ces scénarios, vous pouvez utiliser la propriété tootake de catalogue de données de ressources de données enregistré dans hello catalogue et contrôle hello de visibilité vos actifs de hello. |
| [Supprimer les ressources de données](#remove-data-assets) |Dans cette procédure, vous découvrez comment tooremove les ressources de données à partir de hello catalogue de données. |

## <a name="tutorial-prerequisites"></a>Configuration requise pour le didacticiel
### <a name="azure-subscription"></a>Abonnement Azure
tooset installer Azure Data Catalog, vous devez être propriétaire de hello ou copropriétaire d’un abonnement Azure.

Abonnements Azure permettent d’organiser les ressources du service accès toocloud comme Azure Data Catalog. Ils vous permettent également de contrôler le signalement, la facturation et le paiement des ressources utilisées. Chaque abonnement peut disposer d’une configuration de facturation et de paiement différente. Vous pouvez donc avoir différents abonnements et différents plans par département, projet, bureau régional, etc. Chaque service cloud appartient tooa abonnement, et vous devez toohave un abonnement avant de configurer Azure Data Catalog. toolearn, voir [gérer les comptes, les abonnements et les rôles d’administrateur](../active-directory/active-directory-how-subscriptions-associated-directory.md).

Si vous n'êtes pas abonné, vous pouvez créer un compte d'essai gratuit en quelques minutes. Pour plus d’informations, consultez la page [Version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/) .

### <a name="azure-active-directory"></a>Azure Active Directory
tooset installer Azure Data Catalog, vous devez être connecté avec un compte d’utilisateur Azure Active Directory (Azure AD). Vous devez être propriétaire de hello ou copropriétaire d’un abonnement Azure.  

Azure AD fournit un moyen simple pour votre entreprise toomanage identités et des accès, à la fois dans le cloud de hello et sur site. Vous pouvez utiliser un seul Professionnel ou scolaire compte toosign dans tooany cloud ou local web application. Azure Data Catalog utilise l’authentification dans Azure AD tooauthenticate. toolearn, voir [quoi consiste Azure Active Directory](../active-directory/active-directory-whatis.md).

### <a name="azure-active-directory-policy-configuration"></a>Configuration de la stratégie Azure Active Directory
Vous pouvez rencontrer une situation où vous pouvez vous connecter dans le portail d’Azure Data Catalog toohello, mais lorsque vous essayez de toosign dans l’outil de l’enregistrement de source de données toohello, un message d’erreur qui vous empêche de se connecter. Cette erreur peut se produire lorsque vous êtes sur le réseau d’entreprise hello ou lorsque vous vous connectez à partir du réseau d’entreprise en dehors de hello.

outil d’inscription de Hello utilise *l’authentification par formulaire* toovalidate connexions utilisateur par rapport à Azure Active Directory. Pour la connexion réussie, un administrateur Azure Active Directory doit activer l’authentification par formulaire Bonjour *stratégie d’authentification globale*.

Avec la stratégie d’authentification globale hello, vous pouvez activer l’authentification séparément pour les connexions intranet et extranet, comme indiqué dans hello suivant l’image. Erreurs de connexion peuvent se produire si l’authentification par formulaire n’est pas activée pour le réseau hello à partir de laquelle vous vous connectez.

 ![Stratégie d’authentification globale Azure Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

Pour plus d’informations, consultez [Configuration des stratégies d’authentification](https://technet.microsoft.com/library/dn486781.aspx).

## <a name="provision-data-catalog"></a>Approvisionner Data Catalog
Vous ne pouvez approvisionner qu’un seul catalogue de données par organisation (domaine Azure Active Directory). Par conséquent, si le propriétaire de hello ou d’un abonnement Azure copropriétaire qui appartient toothis domaine Azure Active Directory a déjà créé d’un catalogue, vous pas sera en mesure de toocreate un catalogue à nouveau même si vous avez plusieurs abonnements Azure. tootest si un catalogue de données a été créé par un utilisateur dans votre domaine Azure Active Directory, accédez à toohello [page d’accueil Azure Data Catalog](http://azuredatacatalog.com) et vérifiez si vous disposez de catalogue de hello. Si un catalogue a déjà été créé pour vous, ignorez hello suivant la section suivante de procédure et de passer toohello.    

1. Accédez toohello [page de service de catalogue de données](https://azure.microsoft.com/services/data-catalog) et cliquez sur **prise en main**.
   
    ![Azure Data Catalog--page d’accueil marketing](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Connectez-vous avec un compte d’utilisateur qui est propriétaire de hello ou copropriétaire d’un abonnement Azure. Vous consultez hello suivant page après l’ouverture de session.
   
    ![Azure Data Catalog--approvisionner data catalog](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. Spécifiez un **nom** pour le catalogue de données hello hello **abonnement** vous souhaitez toouse, hello **emplacement** pour le catalogue hello.
4. Développez **Prix appliqués** et sélectionnez une **édition** d’Azure Data Catalog (gratuite ou standard).
    ![Azure Data Catalog--sélectionner édition](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. Développez **utilisateurs catalogue** et cliquez sur **ajouter** tooadd des utilisateurs pour le catalogue de données hello. Vous êtes automatiquement ajouté toothis groupe.
    ![Azure Data Catalog--utilisateurs](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. Développez **les administrateurs de catalogue** et cliquez sur **ajouter** tooadd des administrateurs supplémentaires pour le catalogue de données hello. Vous êtes automatiquement ajouté toothis groupe.
    ![Azure Data Catalog--administrateurs](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. Cliquez sur **créer un catalogue** catalogue de données toocreate hello pour votre organisation. Vous consultez une page d’accueil hello pour le catalogue de données hello après sa création.
    ![Azure Data Catalog--créé](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>Trouver un catalogue de données Bonjour portail Azure
1. Sur un onglet distinct dans le navigateur hello ou dans une fenêtre de navigateur web distinct, accédez à toohello [portail Azure](https://portal.azure.com) et connectez-vous à l’aide hello même compte que vous toocreate utilisé hello catalogue de données à l’étape précédente de hello.
2. Cliquez sur **Parcourir**, puis sur **Catalogue de données**.
   
    ![Azure Data Catalog--Parcourir Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) vous consultez les données de salutation catalogue que vous avez créé.
   
    ![Azure Data Catalog--afficher le catalogue dans une liste](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. Cliquez sur hello catalogue que vous avez créé. Vous consultez hello **Data Catalog** panneau dans le portail de hello.
   
   ![Azure Data Catalog--panneau dans le portail ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. Vous pouvez afficher les propriétés du catalogue de données hello et les mettre à jour. Par exemple, cliquez sur **niveau tarifaire** et changer l’édition de hello.
   
    ![Azure Data Catalog--niveau tarifaire](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Exemple de base de données Adventure Works
Dans ce didacticiel, vous inscrivez des ressources de données (tables) de hello AdventureWorks2014 base de données exemple hello du moteur de base de données SQL Server, mais vous pouvez utiliser n’importe quelle source de données pris en charge si vous préférez toowork par des données pertinentes et familiers tooyour rôle. Pour obtenir la liste des sources de données prises en charge, consultez l’article [Sources de données prises en charge](data-catalog-dsr.md).

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Installer la base de données Adventure Works 2014 OLTP hello
base de données Adventure Works Hello prend en charge les scénarios de traitement transactionnel en ligne standard pour un fabricant de bicyclettes fictive (Adventure Works Cycles), qui inclut les produits, les ventes et d’achat. Dans ce didacticiel, vous inscrivez des informations sur les produits dans Azure Data Catalog.

base de données tooinstall hello Adventure Works exemple :

1. Téléchargez [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) sur CodePlex.
2. base de données toorestore hello sur votre ordinateur, suivez les instructions de hello dans [restaurer une sauvegarde de base de données à l’aide de SQL Server Management Studio](http://msdn.microsoft.com/library/ms177429.aspx), ou en procédant comme suit :
   1. Ouvrez SQL Server Management Studio et connectez-vous toohello du moteur de base de données SQL Server.
   2. Cliquez avec le bouton droit sur **Bases de données**, puis cliquez sur **Restaurer la base de données**.
   3. Sous **restaurer la base de données**, cliquez sur hello **périphérique** est définie sur **Source** et cliquez sur **Parcourir**.
   4. Sous **Sélectionner les unités de sauvegarde**, cliquez sur **Ajouter**.
   5. Dossier de toohello accédez où vous avez hello **AdventureWorks2014.bak** fichier, hello Sélectionnez fichier et cliquez sur **OK** tooclose hello **localiser le fichier de sauvegarde** boîte de dialogue.
   6. Cliquez sur **OK** tooclose hello **sélectionner les unités de sauvegarde** boîte de dialogue.    
   7. Cliquez sur **OK** tooclose hello **restaurer la base de données** boîte de dialogue.

Vous pouvez maintenant inscrire les ressources de données à partir de la base de données exemple hello Adventure Works à l’aide d’Azure Data Catalog.

## <a name="register-data-assets"></a>Inscrire des ressources de données
Dans cet exercice, vous utilisez des ressources de données hello inscription outil tooregister à partir de la base de données Adventure Works hello avec catalogue de hello. Inscription consiste hello extraction clée métadonnées structurelles telles que les noms, les types et les emplacements à partir de la source de données hello et actifs hello qu’il contient et la copie de ce catalogue toohello de métadonnées. Hello source de données et de vos données restent où ils sont, mais les métadonnées de hello sont utilisées par hello catalogue toomake les plus facilement identifiables et plus compréhensible.

### <a name="register-a-data-source"></a>Référencer une source de données
1. Accédez toohello [page d’accueil Azure Data Catalog](http://azuredatacatalog.com) et cliquez sur **publier des données**.
   
   ![Azure Data Catalog--bouton Publier des données](media/data-catalog-get-started/data-catalog-publish-data.png)
2. Cliquez sur **lancer l’Application** toodownload, installation et outil d’inscription de hello d’exécution sur votre ordinateur.
   
   ![Azure Data Catalog--bouton de lancement](media/data-catalog-get-started/data-catalog-launch-application.png)
3. Sur hello **Bienvenue** , cliquez sur **connectez-vous** et entrez vos informations d’identification.     
   
    ![Azure Data Catalog--page d’accueil](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. Sur hello **Microsoft Azure Data Catalog** , cliquez sur **SQL Server** et **suivant**.
   
    ![Azure Data Catalog--sources de données](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Entrez les propriétés de connexion SQL Server hello pour **AdventureWorks2014** (voir hello exemple ci-dessous) et cliquez sur **connexion**.
   
   ![Azure Data Catalog--paramètres de connexion à SQL Server](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. Enregistrer les métadonnées de hello de votre ressource de données. Dans cet exemple, vous inscrivez **Production/produit** objets à partir de l’espace de noms hello AdventureWorks Production :
   
   1. Bonjour **hiérarchie serveur** d’arborescence, développez **AdventureWorks2014** et cliquez sur **Production**.
   2. Appuyez sur la touche CTRL et cliquez sur **Product**, **ProductCategory**, **ProductDescription** et **ProductPhoto**.
   3. Cliquez sur hello **déplacer flèche sélectionnée** (**>**). Cette action déplace tous les objets sélectionnés dans hello **toobe objets inscrits** liste.
      
      ![Didacticiel Azure Data Catalog--parcourir et sélectionner des objets](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. Sélectionnez **incluent un aperçu de** tooinclude un aperçu instantané de données de hello. instantané d’Hello inclut les enregistrements too20 de chaque table, et il est copié dans le catalogue de hello.
   5. Sélectionnez **inclure un profil de données** tooinclude un instantané des statistiques d’objet hello pour le profil de données hello (par exemple : les valeurs minimales, maximales et moyennes pour une colonne, le nombre de lignes).
   6. Bonjour **ajouter des balises** , entrez **adventure fonctionne, les cycles de**. Cette action ajoute des étiquettes de recherche à ces ressources de données. Les balises sont un excellent moyen de toohelp utilisateurs de trouver une source de données inscrits.
   7. Spécifiez le nom hello d’un **expert** sur ces données (facultatives).
      
      ![Didacticiel de catalogue de données Azure--toobe objets inscrits](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. Cliquez sur **INSCRIRE**. Azure Data Catalog enregistre les objets que vous avez sélectionnés. Dans cet exercice, les objets hello sélectionné à partir d’Adventure Works sont inscrits. outil d’inscription de Hello extrait des métadonnées à partir de la ressource de données hello et copie ces données dans le service de catalogue de données Azure hello. Hello données demeurent dans lequel il réside actuellement et reste sous contrôle hello des administrateurs de hello et les stratégies du système en cours de hello.
      
      ![Azure Data Catalog--objets inscrits](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. Cliquez sur vos objets de source de données inscrite, toosee **vue Portal**. Dans le portail Azure Data Catalog hello, vérifiez que tous les quatre tables et la base de données hello dans Affichage de grille hello.
      
      ![Objets dans le portail d’Azure Data Catalog hello ](media/data-catalog-get-started/data-catalog-view-portal.png)

Dans cet exercice, vous avez enregistré les objets de base de données exemple hello Adventure Works afin qu’ils puissent être facilement détectés par les utilisateurs de votre organisation. Dans l’exercice suivant de hello, vous découvrez comment toodiscover des ressources de données référencées.

## <a name="discover-data-assets"></a>Découvrir les ressources de données
Dans Azure Data Catalog, la découverte utilise deux mécanismes principaux : la recherche et le filtrage.

La recherche est conçue toobe intuitif et puissant. Par défaut, les termes de recherche sont mises en correspondance par rapport à n’importe quelle propriété dans le catalogue de hello, y compris les annotations fourni par l’utilisateur.

Le filtrage est conçu toocomplement recherche. Vous pouvez sélectionner des caractéristiques spécifiques telles que les experts, type de source de données, type d’objet, et tooview balises correspondant à des ressources de données et tooconstrain recherche résultats toomatching actifs.

En utilisant une combinaison de recherche et de filtrage, vous pouvez naviguer rapidement des sources de données hello qui ont été inscrits avec des ressources de données Azure Data Catalog toodiscover hello que vous avez besoin.

Dans cet exercice, vous utilisez des ressources de données toodiscover portail Azure Data Catalog hello que vous avez enregistré dans l’exercice précédent de hello. Pour plus d’informations sur la syntaxe de recherche, consultez l’article [Data Catalog Search syntax reference (Informations de référence sur la syntaxe de recherche dans Data Catalog)](https://msdn.microsoft.com/library/azure/mt267594.aspx) .

Voici quelques exemples de découverte des ressources de données dans le catalogue de hello.  

### <a name="discover-data-assets-with-basic-search"></a>Découvrir les ressources de données à l’aide de la fonction de recherche de base
La recherche de base vous permet d’effectuer des recherches dans le catalogue en utilisant un ou plusieurs termes de recherche. Les résultats sont les actifs qui correspond à n’importe quelle propriété avec un ou plusieurs des termes hello spécifiés.

1. Cliquez sur **accueil** dans le portail d’Azure Data Catalog hello. Si vous avez fermé le navigateur web de hello, accédez à toohello [page d’accueil Azure Data Catalog](https://www.azuredatacatalog.com).
2. Dans la zone de recherche de hello, entrez `cycles` et appuyez sur **entrée**.
   
    ![Azure Data Catalog--recherche de texte de base](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. Vérifiez que toutes les quatre tables et la base de données de hello (AdventureWorks2014) dans les résultats de hello. Vous pouvez basculer entre **affichage de grille** et **mode liste** en cliquant sur les boutons de barre d’outils hello comme indiqué dans hello suivant l’image. Notez ce mot clé de recherche hello est mis en surbrillance dans les résultats de recherche hello car hello **mettre en surbrillance** option est **ON**. Vous pouvez également spécifier le nombre de hello de **résultats par page** dans les résultats de la recherche.
   
    ![Azure Data Catalog--résultats de recherche de texte de base](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    Hello **recherche** Panneau de configuration se trouve sur hello gauche et hello **propriétés** Panneau de configuration se trouve sur hello droite. Sur hello **recherche** Panneau de configuration, vous pouvez modifier les critères de recherche et filtrer les résultats. Hello **propriétés** panneau affiche les propriétés d’un objet sélectionné dans la grille de hello ou liste.
4. Cliquez sur **produit** dans les résultats de recherche hello. Cliquez sur hello **aperçu**, **colonnes**, **profil des données**, et **Documentation** onglets, ou cliquez sur le volet inférieur hello hello flèche tooexpand.  
   
    ![Azure Data Catalog--volet inférieur](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    Sur hello **aperçu** onglet, vous consultez un aperçu des données hello Bonjour **produit** table.  
5. Cliquez sur hello **colonnes** onglet toofind plus d’informations sur les colonnes (tels que **nom** et **type de données**) dans la ressource de données hello.
6. Cliquez sur hello **profil des données** onglet toosee hello de profilage des données (par exemple : nombre de lignes, la taille des données ou la valeur minimale dans une colonne) dans la ressource de données hello.
7. Filtrer les résultats de hello à l’aide de **filtres** sur hello gauche. Par exemple, cliquez sur **Table** pour **Type d’objet**, et que vous consultez seules les tables hello quatre, hello pas de base de données.
   
    ![Azure Data Catalog--filtrer les résultats de recherche](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>Découvrir les ressources de données à l’aide de la fonction de recherche d’étendue de la propriété
Propriété étendue permet de surveiller les ressources de données où le terme de recherche hello est mis en correspondance avec hello de propriété spécifiée.

1. Désactivez hello **Table** filtrer sous **Type d’objet** dans **filtres**.  
2. Dans la zone de recherche de hello, entrez `tags:cycles` et appuyez sur **entrée**. Consultez [référence de syntaxe de recherche de catalogue de données](https://msdn.microsoft.com/library/azure/mt267594.aspx) pour tous les hello propriétés que vous pouvez utiliser pour la recherche de catalogue de données hello.
3. Vérifiez que toutes les quatre tables et la base de données de hello (AdventureWorks2014) dans les résultats de hello.  
   
    ![Data Catalog--résultats de recherche d’étendue de la propriété](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Enregistrer la recherche de hello
1. Bonjour **recherche** volet Bonjour **recherche actuelle** , entrez un nom pour la recherche de hello et cliquez sur **enregistrer**.
   
    ![Azure Data Catalog--enregistrer la recherche](media/data-catalog-get-started/data-catalog-save-search.png)
2. Vérifiez que la recherche hello enregistré s’affiche sous **recherches enregistrées**.
   
    ![Azure Data Catalog--recherches enregistrées](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Sélectionnez une des actions à entreprendre sur la recherche de hello enregistré hello (**renommer**, **supprimer**, **enregistrer par défaut** recherche).
   
    ![Azure Data Catalog--options de recherche enregistrées](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>Opérateurs booléens
Vous pouvez élargir ou affiner votre recherche à l’aide des opérateurs booléens.

1. Dans la zone de recherche de hello, entrez `tags:cycles AND objectType:table`, puis appuyez sur **entrée**.
2. Vérifiez que vous voyez uniquement les tables (pas hello de base de données) dans les résultats de hello.  
   
    ![Azure Data Catalog--opérateur booléen dans la recherche](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>Parenthèses de regroupement
En effectuant un regroupement avec des parenthèses, vous pouvez regrouper des parties de hello requête tooachieve d’isolation logique, en particulier, ainsi que des opérateurs booléens.

1. Dans la zone de recherche de hello, entrez `name:product AND (tags:cycles AND objectType:table)` et appuyez sur **entrée**.
2. Vérifiez que vous voyez uniquement hello **produit** table dans les résultats de recherche hello.
   
    ![Azure Data Catalog--recherche par regroupement](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>Opérateurs de comparaison
Les opérateurs de comparaison vous permettent d’utiliser des comparaisons autres que l’égalité pour les propriétés comportant des types de données numériques et de date.

1. Dans la zone de recherche de hello, entrez `lastRegisteredTime:>"06/09/2016"`.
2. Désactivez hello **Table** filtrer sous **Type d’objet**.
3. Appuyez sur **ENTRÉE**.
4. Vérifiez que vous voyez hello **produit**, **ProductCategory**, **ProductDescription**, et **ProductPhoto** hello et tables La base de données AdventureWorks2014 que vous enregistré dans les résultats de la recherche.
   
    ![Azure Data Catalog--résultats de recherche par comparaison](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

Consultez [comment les ressources de données toodiscover](data-catalog-how-to-discover.md) pour plus d’informations sur la détection des ressources de données et [référence de syntaxe de recherche de catalogue de données](https://msdn.microsoft.com/library/azure/mt267594.aspx) pour la syntaxe de recherche.

## <a name="annotate-data-assets"></a>Annoter les ressources de données
Dans cet exercice, vous utilisez tooannotate de portail Azure Data Catalog hello (ajouter des informations telles que des descriptions, des étiquettes ou des experts) des ressources de données que vous avez déjà enregistré dans le catalogue de hello. les annotations Hello complément et améliorent les métadonnées structurelles hello extraites à partir de la source de données hello lors de l’inscription et rend les ressources de données hello beaucoup plus facile toodiscover et comprennent.

Dans cet exercice, vous annotez une ressource de données unique (ProductPhoto). Vous ajoutez un nom convivial et une ressource de données de description toohello ProductPhoto.  

1. Accédez toohello [page d’accueil Azure Data Catalog](https://www.azuredatacatalog.com) et de recherche avec `tags:cycles` toofind hello données de l’entreprise que vous avez enregistré.  
2. Cliquez sur **ProductPhoto** dans les résultats de la recherche.  
3. Entrez **des images** pour **nom convivial** et **photos de produit pour la commercialisation des matériaux** pour hello **Description**.
   
    ![Azure Data Catalog--description d’une photo de produit](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    Hello **Description** permet aux autres utilisateurs de découvrir et de comprendre pourquoi et comment toouse hello sélectionné la ressource de données. Vous pouvez également ajouter des balises supplémentaires et afficher les colonnes. Maintenant vous pouvez essayer de ressources de données toodiscover recherche et de filtrage à l’aide des métadonnées descriptives de hello, vous avez ajouté toohello catalogue.

Vous pouvez également effectuer hello suivant sur cette page :

* Ajouter des experts pour la ressource de données hello. Cliquez sur **ajouter** Bonjour **Experts** zone.
* Ajouter des balises au niveau de jeu de données hello. Cliquez sur **ajouter** Bonjour **balises** zone. Une balise peut être une balise utilisateur ou une balise glossaire. Hello Data Catalog Standard inclut un glossaire métier qui permet aux administrateurs de catalogue définissent une taxonomie commerciales. Les utilisateurs du catalogue peuvent ensuite annoter les ressources de données avec la terminologie du glossaire. Pour plus d’informations, consultez [comment tooset des hello glossaire métier pour baliser les régie](data-catalog-how-to-business-glossary.md)
* Ajouter des balises au niveau de colonne hello. Cliquez sur **ajouter** sous **balises** pour la colonne de hello souhaité tooannotate.
* Ajoutez la description au niveau de colonne hello. Entrez une **description** pour une colonne. Vous pouvez également afficher les métadonnées de description hello extraites à partir de la source de données hello.
* Ajouter **demander l’accès** information qui indique aux utilisateurs comment toorequest accéder aux ressources de données toohello.
  
    ![Azure Data Catalog--ajouter des balises, des descriptions](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Choisissez hello **Documentation** onglet et fournir une documentation pour la ressource de données hello. Documentation d’Azure Data Catalog, vous pouvez utiliser votre catalogue de données comme un référentiel de contenu de toocreate une narration complète de vos ressources de données.
  
    ![Azure Data Catalog--onglet Documentation](media/data-catalog-get-started/data-catalog-documentation.png)

Vous pouvez également ajouter des ressources toomultiple une annotation. Par exemple, vous pouvez sélectionner tous les éléments de données hello que vous vous êtes inscrit et spécifier un expert pour eux.

![Azure Data Catalog--annoter plusieurs ressources de données](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Azure Data Catalog prend en charge une tooannotations approche rurale surcharger. N’importe quel utilisateur du catalogue de données peut ajouter des descriptions (utilisateur ou glossaire), de balises et d’autres métadonnées, afin que tout utilisateur disposant d’un point de vue sur une ressource de données et son utilisation peut compter cette perspective capturées et tooother disponibles.

Consultez [comment les ressources de données tooannotate](data-catalog-how-to-annotate.md) pour des informations détaillées sur l’annotation des ressources de données.

## <a name="connect-toodata-assets"></a>Se connecter toodata actifs
Dans cet exercice, vous ouvrez les ressources de données dans un outil client intégré (Excel) et dans un outil non intégré (SQL Server Management Studio) à l’aide des informations de connexion.

> [!NOTE]
> Il est important de tooremember Azure Data Catalog ne vous donne pas accéder à la source de données réelles de toohello — il simplement facilite vous toodiscover et comprendre. Lorsque vous vous connectez la source de données tooa, hello application cliente que vous choisissez utilise votre Windows les informations d’identification ou vous invite aux informations d’identification si nécessaire. Si vous n'avez pas déjà été accordé source de données access toohello, vous devez toobe accordé l’accès avant de vous connecter.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Connecter la ressource de données tooa à partir d’Excel
1. Sélectionnez **Produit** dans les résultats de la recherche. Cliquez sur **ouvrir dans** sur la barre d’outils hello et cliquez sur **Excel**.
   
    ![Azure Data Catalog--connecter toodata actif](media/data-catalog-get-started/data-catalog-connect1.png)
2. Cliquez sur **ouvrir** dans la fenêtre contextuelle de téléchargement hello. Cette expérience peut varier selon le navigateur de hello.
   
    ![Azure Data Catalog--télécharger un fichier de connexion Excel](media/data-catalog-get-started/data-catalog-download-open.png)
3. Bonjour **avis de sécurité Microsoft Excel** fenêtre, cliquez sur **activer**.
   
    ![Azure Data Catalog--fenêtre contextuelle de sécurité Excel](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Conserver les valeurs par défaut hello Bonjour **importer des données** boîte de dialogue et cliquez sur **OK**.
   
    ![Azure Data Catalog--données d’importation Excel](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Afficher la source de données hello dans Excel.
   
    ![Azure Data Catalog--table de produits dans Excel](media/data-catalog-get-started/data-catalog-connect2.png)

Dans cet exercice, vous connecté actifs toodata découverts à l’aide d’Azure Data Catalog. Avec le portail d’Azure Data Catalog hello, vous pouvez vous connecter directement à l’aide d’applications clientes de hello intégrées hello **ouvert dans** menu. Vous pouvez également vous connecter avec toute application que vous choisissez à l’aide des informations d’emplacement de connexion hello incluses dans les métadonnées des ressources hello. Par exemple, vous pouvez utiliser des données hello tooaccess de la base de données SQL Server Management Studio tooconnect toohello AdventureWorks2014 dans les ressources de données hello inscrits dans ce didacticiel.

1. Ouvrez **SQL Server Management Studio**.
2. Bonjour **connecter tooServer** boîte de dialogue, entrez le nom du serveur hello de hello **propriétés** volet dans le portail d’Azure Data Catalog hello.
3. Utilisez la ressource de données d’informations d’identification tooaccess hello et d’authentification. Si vous n’avez pas accès, utilisez les informations de hello **demande d’accès** champ tooget il.
   
    ![Azure Data Catalog--demander l’accès](media/data-catalog-get-started/data-catalog-request-access.png)

Cliquez sur **afficher les chaînes de connexion** tooview et copie ADF.NET, ODBC et OLEDB connexion chaînes toohello Presse-papiers pour une utilisation dans votre application.

## <a name="manage-data-assets"></a>Gérer les ressources de données
Dans cette étape, vous voyez comment tooset la sécurité pour vos ressources de données. Catalogue de données ne donne pas les utilisateurs accéder aux données de toohello lui-même. propriétaire Hello hello de source de données contrôle l’accès aux données.

Vous pouvez utiliser le catalogue de données toodiscover des sources de données et métadonnées de hello tooview liés sources toohello inscrits dans le catalogue de hello. Il peut arriver, toutefois, dans lequel les sources de données doivent être uniquement visible toospecific utilisateurs ou toomembers de groupes spécifiques. Pour ces scénarios, vous pouvez utiliser la propriété tootake de catalogue de données de ressources de données enregistré dans le catalogue de hello et la visibilité de hello toothen contrôle de vos actifs de hello.

> [!NOTE]
> fonctionnalités de gestion Hello décrites dans cet exercice sont uniquement disponibles dans hello Édition Standard d’Azure Data Catalog, pas dans hello édition gratuite.
> Dans Azure Data Catalog, vous pouvez prendre possession des ressources de données, ajouter copropriétaires toodata actifs et définir la visibilité de hello de ressources de données.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>S’approprier les ressources de données et restreindre leur visibilité
1. Accédez toohello [page d’accueil Azure Data Catalog](https://www.azuredatacatalog.com). Bonjour **recherche** texte, entrez `tags:cycles` et appuyez sur **entrée**.
2. Cliquez sur un élément dans la liste des résultats hello et cliquez sur **Take Ownership** sur la barre d’outils hello.
3. Bonjour **gestion** section Hello **propriétés** du panneau, cliquez sur **Take Ownership**.
   
    ![Azure Data Catalog--prendre possession](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. toorestrict visibilité, choisissez **propriétaires & ces utilisateurs** Bonjour **visibilité** et cliquez sur **ajouter**. Entrez les adresses de messagerie d’utilisateur dans la zone de texte hello et appuyez sur **entrée**.
   
    ![Azure Data Catalog--restreindre l’accès](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>Supprimer les ressources de données
Dans cet exercice, vous utilisez hello Azure Data Catalog tooremove portail aperçu des données à partir des données et supprimez des ressources de données à partir du catalogue de hello.

Dans Azure Data Catalog, vous pouvez supprimer une ou plusieurs ressources.

1. Accédez toohello [page d’accueil Azure Data Catalog](https://www.azuredatacatalog.com).
2. Bonjour **recherche** texte, entrez `tags:cycles` et cliquez sur **entrée**.
3. Sélectionnez un élément dans la liste des résultats hello et cliquez sur **supprimer** barre d’outils hello comme indiqué dans hello suivant image :
   
    ![Azure Data Catalog--supprimer un élément de grille](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Si vous utilisez l’affichage de liste de hello, case à cocher hello est gauche toohello d’élément de hello, comme indiqué dans hello suivant image :
   
    ![Azure Data Catalog--supprimer un élément de liste](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    Vous pouvez également sélectionner plusieurs ressources de données et les supprimer, comme indiqué dans hello suivant image :
   
    ![Azure Data Catalog--supprimer plusieurs ressources de données](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> Hello le comportement par défaut du catalogue de hello est tooallow tooregister de n’importe quel utilisateur de toute source de données et tooallow toodelete de n’importe quel utilisateur n’importe quel élément de données qui a été inscrit. fonctionnalités de gestion Hello incluses dans l’Édition Standard d’Azure Data Catalog de hello offrent des options supplémentaires pour prendre possession d’actifs, la restriction qui peut découvrir les ressources et en limitant les qui peut supprimer des ressources.
> 
> 

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez exploré les fonctionnalités essentielles d’Azure Data Catalog, notamment l’inscription, l’annotation, la découverte et la gestion des ressources de données d’entreprise. Maintenant que vous avez terminé le didacticiel de hello, il est temps tooget a démarré. Vous pouvez commencer dès aujourd'hui en inscrivant votre équipe et s’appuient sur des sources de données hello et en invitant le catalogue de vos collègues toouse hello.

## <a name="references"></a>Références
* [Comment les ressources de données tooregister](data-catalog-how-to-register.md)
* [Comment les ressources de données toodiscover](data-catalog-how-to-discover.md)
* [Comment les ressources de données tooannotate](data-catalog-how-to-annotate.md)
* [Comment les ressources de données toodocument](data-catalog-how-to-documentation.md)
* [Comment tooconnect toodata actifs](data-catalog-how-to-connect.md)
* [Comment les ressources de données toomanage](data-catalog-how-to-manage.md)

