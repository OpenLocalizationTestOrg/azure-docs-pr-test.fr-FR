---
title: "aaaGuide toocreating un Service de données pour hello Marketplace | Documents Microsoft"
description: "Comment toocreate, certifier et déployer un Service de données pour obtenir des instructions détaillées d’achat sur hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Présentation du schéma de nœuds hello pour mapper un tooOData de service web existant via CSDL
> [!IMPORTANT]
> **À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.** Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners). Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

Ce document vous aide à clarifier la structure de nœud hello pour mapper un tooCSDL de protocole OData. Il est important de toonote que la structure de nœuds hello est bien formé XML. Par conséquent, le schéma racine, parent et enfant s’applique lors de la conception de votre mappage OData.

## <a name="ignored-elements"></a>Éléments ignorés
Hello Voici hello haute CSDL éléments level (nœuds XML) qui ne vont pas toobe utilisée par serveur principal de hello Azure Marketplace pendant l’importation de hello de métadonnées du service web de hello. Ils peuvent être présents, mais seront ignorés.

| Élément | Portée |
| --- | --- |
| Élément Using |nœud de Hello, les sous-nœuds et tous les attributs |
| Élément Documentation |nœud de Hello, les sous-nœuds et tous les attributs |
| ComplexType |nœud de Hello, les sous-nœuds et tous les attributs |
| Élément Association |nœud de Hello, les sous-nœuds et tous les attributs |
| Propriété Extended |nœud de Hello, les sous-nœuds et tous les attributs |
| EntityContainer |Uniquement hello attributs suivants sont ignorés : *étend* et *AssociationSet* |
| Schéma |Uniquement hello attributs suivants sont ignorés : *Namespace* |
| FunctionImport |Uniquement hello attributs suivants sont ignorés : *Mode* (valeur par défaut de ln est utilisée) |
| EventType |Uniquement hello sous-nœuds suivants sont ignorés : *clé* et *PropertyRef* |

Hello la section suivante décrit hello modifications (ajouté et ignorés éléments) toohello différents nœuds CSDL XML en détail.

## <a name="functionimport-node"></a>Nœud FunctionImport
Un nœud FunctionImport représente une URL (point d’entrée) qui expose un utilisateur final toohello de service. nœud de Hello permet de décrire comment hello URL est traité, les paramètres sont l’utilisateur final toohello disponibles et comment ces paramètres sont fournis.

Vous trouverez des informations sur ce nœud [ici][MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx)

Hello suivants sont des attributs supplémentaires hello (ou ajouts tooattributes) qui sont exposées par le nœud de FunctionImport hello :

**d:baseUri** -modèle d’URI hello pour ressource REST hello tooMarketplace exposé. Marketplace utilise hello modèle tooconstruct interrogations hello service web REST. modèle d’URI Hello contient des espaces réservés pour les paramètres de hello sous forme hello {parameterName}, où nom_paramètre désigne hello paramètre hello. P. apiVersion={apiVersion}.
Les paramètres sont autorisés tooappear en tant que paramètres d’URI ou en tant que partie du chemin d’accès URI de hello. Dans les cas de hello d’apparence hello dans le chemin d’accès de hello, ils sont toujours obligatoires (ne peut pas être marquée comme nullable). *Exemple :*`d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Nom** -nom hello Hello de fonction importée.  Ne peut pas être hello identique à celui des autres noms définis dans hello CSDL.  P. ex., Name="GetModelUsageFile"

**EntitySet** *(facultatif)* - si la fonction hello retourne une collection de types d’entités, d’une valeur de hello Hello **EntitySet** doit être une collection hello toowhich de jeu d’entités hello appartient. Dans le cas contraire, hello **EntitySet** attribut ne doit pas être utilisé. *Exemple :*`EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(facultatif)* -Spécifie le type hello d’éléments retournés par hello URI.  N’utilisez pas cet attribut si la fonction hello ne retourne pas de valeur. Hello Voici les types hello pris en charge :

* **Collection (<Entity type name>)** : spécifie une collection de types d’entités définis. nom de Hello est présent dans l’attribut de nom hello du nœud de EntityType hello. Par exemple, Collection(WXC.HourlyResult).
* **Brut (<mime type>)**: Spécifie un document/blob brut qui est retourné toohello utilisateur. Par exemple, Raw(image/jpeg) ; autres exemples :

  * ReturnType="Raw(text/plain)"
  * ReturnType="Collection(sage.DeleteAllUsageFilesEntity)"*

**d:paging** -spécifie comment la pagination est gérée par hello ressource REST. Hello paramètre valeurs sont utilisées dans des branches, par exemple, la page = {$page} & itemsperpage = hello {$size} options disponibles sont :

* **None :** aucune pagination n’est disponible
* **Skip :** la pagination est exprimée à l’aide d’une logique « skip » et « take » (supérieure). Skip saute take et M éléments puis retourne hello suivant N éléments. Valeur du paramètre : $skip
* **Take :** Take retourne hello suivant N éléments. Valeur du paramètre : $take
* **PageSize :** la pagination est exprimée via une page logique et via la taille (éléments par page). Page représente la page actuelle hello est retourné. Valeur du paramètre : $page
* **Taille :** taille représente le nombre de hello d’éléments renvoyés pour chaque page. Valeur du paramètre : $size

**d:AllowedHttpMethods** *(facultatif)* -Spécifie le verbe est géré par la ressource REST hello. Aussi, restreint toohello acceptée verbe spécifié valeur.  Valeur par défaut = POST.  *Exemple :* `d:AllowedHttpMethods="GET"` hello les options disponibles sont :

* **GET :** généralement utilisé tooreturn données
* **VALIDER :** généralement utilisé tooinsert de nouvelles données
* **PUT :** généralement utilisé tooupdate données
* **SUPPRESSION :** utilisé toodelete des données

Les nœuds enfants supplémentaires (non couverts par la documentation de CSDL hello) dans le nœud de FunctionImport hello sont :

**d:RequestBody** *(facultatif)* -demande hello corps est utilisé tooindicate qui hello demande attend un toobe corps envoyé. Paramètres peuvent être données au sein du corps de la demande hello. Ils sont exprimés dans des accolades, p. ex., {parameterName}. Ces paramètres sont mappés de hello l’entrée d’utilisateur dans le corps de hello est transféré service du fournisseur de contenu toohello. élément de requestBody Hello possède un attribut avec le nom httpMethod. attribut de Hello permet à deux valeurs :

* **VALIDER :** utilisé si la demande de hello est une demande HTTP POST
* **GET :** utilisé si la demande de hello est un HTTP GET

    Exemple :

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:Namespaces** et **d:Namespace** -ce nœud décrit hello des espaces de noms qui sont définis dans hello XML qui est retourné par l’importation de fonction hello (point de terminaison URI). Hello XML qui est retourné par le service principal de hello peut contenir n’importe quel nombre d’espaces de noms toodifferentiate hello contenu qui est retourné. **Tous ces espaces de noms, si utilisée dans les requêtes XPath d:Map ou d:Match doivent toobe répertorié.** nœud d:Namespaces de Hello contient une liste définie/de d:Namespace nœuds. Chacun d’eux répertorie un espace de noms utilisé dans la réponse du service principal hello. Hello Voici attribut hello du nœud de d:Namespace hello :

* **d:prefix :** hello préfixe d’espace de noms hello, comme dans hello XML des résultats retournés par le service de hello, par exemple, f:FirstName, f:LastName, où f est le préfixe de hello.
* **d:URI :** hello URI complet de l’espace de noms hello utilisé dans le document de résultats hello. Il représente la valeur de hello ce préfixe hello est résolu tooat runtime.

**d:ErrorHandling***(facultatif)* : ce nœud contient des conditions pour la gestion des erreurs. Chacune des conditions de hello est validé par rapport aux résultats hello qui est retourné par le service du fournisseur de contenu hello. Si une condition est remplie hello proposé le code d’erreur HTTP un message d’erreur est retourné par l’utilisateur toohello.

**d:ErrorHandling** *(facultatif)* et **d:Condition** *(facultatif)* -le nœud de condition conserve une seule condition est vérifiée dans le résultat de hello retourné par service de Hello du fournisseur. Hello Voici hello **requis** attributs :

* **d:match :** XML de sortie de l’expression XPath qui vérifie si une nœud/valeur donnée n’est présente dans le fournisseur de contenu hello. Hello XPath est exécutée sur la sortie de hello et doit retourner true si la condition de hello est une correspondance ou une valeur false dans le cas contraire.
* **d:HttpStatusCode :** hello le code d’état HTTP doit être retourné par Marketplace correspond aux critères de condition de cas hello hello. Marketplace signalizes utilisateur de toohello erreurs via des codes d’état HTTP. Une liste des codes d’état HTTP est disponible à l’adresse http://en.wikipedia.org/wiki/HTTP_status_code
* **d:ErrorMessage :** message d’erreur hello est l’utilisateur final retourné – avec le code d’état HTTP de hello – toohello. Il s’agit d’un message d’erreur amical qui ne contient aucun secret.

**d:Title** *(facultatif)* -permettant de décrire le titre hello de fonction hello. valeur Hello pour le titre de hello provient

* Hello optionnel attribut (xpath) qui spécifie où le titre de hello toofind dans la réponse de hello retournés à partir de la demande de service hello.
* - Ou - titre hello spécifié en tant que valeur du nœud de hello.

**d:Rights** *(facultatif)* -hello droits (par exemple, copyright) associés à fonction hello. valeur Hello pour les droits de hello provient :

* Hello optionnel attribut (xpath) qui spécifie où les droits de hello toofind dans la réponse de hello retournés à partir de la demande de service hello.
* - Ou - droits hello spécifiés en tant que valeur du nœud de hello.

**d:description** *(facultatif)* - une brève description de la fonction hello. valeur Hello pour la description hello provient

* Hello optionnel attribut (xpath) qui spécifie où la description de hello toofind dans la réponse de hello retournés à partir de la demande de service hello.
* - Ou -description hello spécifié en tant que valeur du nœud de hello.

**d:EmitSelfLink** - *consultez l’exemple ci-dessus « FunctionImport pour la pagination » via les données renvoyées*

**d:EncodeParameterValue** -tooOData d’extension facultative

**d:QueryResourceCost** -tooOData d’extension facultative

**d:Map** -tooOData d’extension facultative

**d:Headers** -tooOData d’extension facultative

**d:Headers** -tooOData d’extension facultative

**d:value** -tooOData d’extension facultative

**d:HttpStatusCode** -tooOData d’extension facultative

**d:ErrorMessage** -tooOData d’Extension facultative

## <a name="parameter-node"></a>Nœud du paramètre
Ce nœud représente un paramètre qui est exposé en tant que partie du modèle d’URI hello / corps a été spécifié dans le nœud de FunctionImport hello de la demande.

Une page de document très utile pour plus d’informations sur le nœud de « Élément de paramètre » hello se trouvant à [ici](http://msdn.microsoft.com/library/ee473431.aspx) (hello d’utilisation **Version autres** tooselect de liste déroulante une version différente si nécessaire tooview hello documentation). *Exemple :*`<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| Attribut de paramètre | Est obligatoire | Valeur |
| --- | --- | --- |
| Name |Oui |nom de Hello du paramètre hello. Respecte la casse.  Respecter la casse de BaseUri hello. **Exemple :**`<Property Name="IsDormant" Type="Byte" />` |
| Type |Oui |type de paramètre Hello. la valeur Hello doit être un **EDMSimpleType** ou un type complexe qui est étendue hello du modèle de hello. Pour plus d’informations, consultez « 6. Types de paramètres/propriétés pris en charge ».  (Respecte la casse. Le premier caractère est en majuscule, les autres sont en minuscules).  Voir également [Types de modèle conceptuel (CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx). **Exemple :**`<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Mode |Non |**Dans**, Out ou InOut selon si le paramètre hello est un paramètre d’entrée, sortie ou d’entrée/sortie. (Seule la valeur « IN » est disponible dans Azure Marketplace.) **Exemple :**`<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| MaxLength |Non |Hello longueur maximale autorisée de paramètre hello. **Exemple :**`<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| Precision |Non |précision de Hello de paramètre hello. **Exemple :**`<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Mettre à l'échelle |Non |échelle de Hello du paramètre hello. **Exemple :**`<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

Hello hello les attributs qui ont été ajoutés spécification CSDL de toohello sont :

| Attribut de paramètre | Description |
| --- | --- |
| **d:Regex***(facultatif)* |Une instruction d’expression régulière utilisé la valeur d’entrée de toovalidate hello pour le paramètre hello. Si la valeur d’entrée de hello ne correspond pas à valeur de hello instruction hello est rejetée. Cela permet de toospecify également un ensemble de valeurs possibles, par exemple, ^ [0-9] + ? $ tooonly autorise les numéros. **Exemple :** `&lt;Parameter Name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="Un nom qui ne peut pas contenir des espaces ou des caractères non anglais" d:SampleValues="George |
| **d:Enum***(facultatif)* |Un canal de communication liste séparée par des valeurs valides pour le paramètre hello. type Hello des valeurs de hello doit toomatch hello défini par type de hello paramètre. Exemple : `anglais |
| **d:Nullable***(facultatif)* |Permet de définir si un paramètre peut être null. valeur par défaut Hello est : true. Toutefois, les paramètres qui sont exposées en tant que partie du chemin d’accès de hello dans le modèle d’URI hello ne peut pas être null. Lors de l’attribut de hello a la valeur toofalse pour ces paramètres – hello l’entrée d’utilisateur est remplacée. **Exemple :**`<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue***(facultatif)* |Un toodisplay valeur exemple comme un Client de toohello Remarque Bonjour l’interface utilisateur.  Il est possible de répertorier tooadd séparés de plusieurs valeurs à l’aide d’un canal de communication, par exemple, « un |

## <a name="entitytype-node"></a>Nœud EntityType
Ce nœud représente un des types de hello sont retournées à partir de l’utilisateur final de toohello Marketplace. Il contient également le mappage hello à partir de la sortie hello qui est retourné par les valeurs du fournisseur de contenu hello service toohello qui sont retournées par l’utilisateur toohello.

Plus d’informations sur ce nœud sont trouvent dans [ici](http://msdn.microsoft.com/library/bb399206.aspx) (hello d’utilisation **Version autres** tooselect de liste déroulante une version différente si nécessaire tooview hello documentation.)

| Nom de l'attribut | Est obligatoire | Valeur |
| --- | --- | --- |
| Name |Oui |nom Hello hello du type d’entité. **Exemple :**`<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |Non |nom Hello d’un autre type d’entité qui est le type de base hello hello du type d’entité qui est défini. **Exemple :**`<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

Hello hello les attributs qui ont été ajoutés spécification CSDL de toohello sont :

**d:Map** -expression XPath exécutée sur la sortie du service hello. Hello hypothèse est que sortie hello du service contient un ensemble d’éléments qui se répètent, comme un ATOM flux où il existe un ensemble de nœuds d’entrée qui se répètent. Chacun de ces nœuds qui se répètent contient un enregistrement. Hello XPath est spécifiée toopoint au nœud répété de hello individuels dans les résultats du service du fournisseur de contenu hello qui contient les valeurs hello un enregistrement individuel. Exemple de sortie à partir du service de hello :

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

Hello expression XPath serait /foo/bar, car chaque nœud de barre hello est hello nœud Bonjour de sortie, et il contient le contenu réel hello qui est retourné par l’utilisateur toohello extensibles.

**Key** : cet attribut est ignoré par Marketplace. En général, les services web basés sur REST n’exposent pas de clé primaire.

## <a name="property-node"></a>Nœud de propriété
Ce nœud contient une propriété de l’enregistrement de hello.

Plus d’informations sur ce nœud sont trouvent dans [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (hello d’utilisation **Version autres** tooselect de liste déroulante une version différente si nécessaire tooview hello documentation.) *Exemple :*`<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| Nom de l’attribut | obligatoires | Valeur |
| --- | --- | --- |
| Name |Oui |nom de Hello de propriété de hello. |
| Type |Oui |type Hello hello de valeur de propriété. type de valeur de propriété Hello doit être un **EDMSimpleType** ou un type complexe (indiqué par un nom qualifié complet) qui se trouve dans l’étendue du modèle de hello. Pour plus d’informations, consultez Types de modèle conceptuel (CSDL). |
| Nullable |Non |**True** (hello la valeur par défaut) ou **False** selon si la propriété de hello peut avoir une valeur null. Remarque : Bonjour version de CSDL indiqué par hello [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) espace de noms, une propriété de type complexe doit avoir Nullable = « False ». |
| DefaultValue |Non |valeur par défaut de Hello de propriété de hello. |
| MaxLength |Non |longueur maximale de Hello hello de valeur de propriété. |
| FixedLength |Non |**True** ou **False** selon si valeur de propriété hello est stockée comme une chaîne de longueur fiexed. |
| Precision |Non |Désigne le nombre maximal de toohello de tooretain de chiffres dans la valeur numérique de hello. |
| Mettre à l'échelle |Non |Nombre maximal de tooretain du nombre de décimales dans la valeur numérique de hello. |
| Unicode |Non |**True** ou **False** selon que la valeur de la propriété hello être stockées sous forme de chaîne Unicode. |
| Collation |Non |Chaîne qui spécifie hello toobe séquence utilisé dans la source de données hello de classement. |
| ConcurrencyMode |Non |**Aucun** (hello la valeur par défaut) ou **fixe**. Si la valeur de hello a trop**fixe**, valeur de la propriété hello sera utilisé dans les contrôles d’accès concurrentiel optimiste. |

Hello hello des attributs supplémentaires qui ont été ajoutés spécification CSDL de toohello sont :

**d:Map** -expression XPath exécutée sur le service de hello de sortie et extrait une propriété de sortie de hello. Hello XPath spécifié est relatif toohello noeud qui a été sélectionné dans les XPath du nœud hello EntityType extensible. Il est également possible toospecify un tooallow XPath absolue, y compris une ressource statique dans chacune des hello sortie nœuds, comme par exemple une déclaration de copyright qui se trouve uniquement une fois Bonjour service d’origine de sortie, mais doit être présent dans chacune des lignes hello Bonjour OData sortie. Exemple de service de hello :

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

expression XPath Hello serait un nœud de baz0 ./bar/baz0 tooget hello du service du fournisseur de contenu hello.

**d:CharMaxLength** -pour le type de chaîne, vous pouvez spécifier la longueur maximale hello. Consultez l’exemple de service de données CSDL.

**d:IsPrimaryKey** -indique si la colonne de hello est clé primaire de hello dans la table ou de vue hello. Consultez l’exemple de service de données CSDL.

**d:isExposed** -détermine si le schéma de la table hello est exposé (généralement true). Consultez l’exemple de service de données CSDL.

**d:IsView***(facultatif)* : valeur true si cela est basé sur une vue plutôt que sur une table.  Consultez l’exemple de service de données CSDL.

**d:Tableschema** : consultez l’exemple de service de données CSDL.

**d:ColumnName** -nom hello de colonne hello dans la table ou de vue hello.  Consultez l’exemple de service de données CSDL.

**d:IsReturned** -est hello booléen qui détermine si hello Service expose ce client toohello de valeur.  Consultez l’exemple de service de données CSDL.

**d:IsQueryable** -est hello valeur booléenne qui détermine si la colonne de hello peut être utilisé dans une requête de base de données.   Consultez l’exemple de service de données CSDL.

**d:OrdinalPosition** -est hello numérique position de la colonne de l’apparence, x, dans la table de hello ou une vue de hello, où x correspond à partir du numéro 1 toohello des colonnes de table de hello.  Consultez l’exemple de service de données CSDL.

**d:DatabaseDataType** -hello type de données de colonne hello dans la base de données hello, autrement dit, le type de données SQL. Consultez l’exemple de service de données CSDL.

## <a name="supported-parametersproperty-types"></a>Types de paramètres/propriétés pris en charge
Hello Voici les types hello pris en charge pour les paramètres et propriétés. (Respectent la casse)

| Types primitifs | Description |
| --- | --- |
| Null |Représente l’absence de hello d’une valeur |
| Boolean |Représente le concept mathématique de hello de logique binaire |
| Byte |Valeur entière 8 bits non signée |
| DateTime |Représente la date et l’heure avec des valeurs allant de 12:00:00 (minuit), le 1er janvier 1753 (après Jésus-Christ) à 11:59:59 (soir), décembre 9999 (après Jésus-Christ) |
| Décimal |Représente des valeurs numériques avec précision et échelle fixes. Ce type peut décrire une valeur numérique comprise entre-10 ^ toopositive 255 + 1 10 ^-255 1 |
| Double |Représente un nombre à virgule flottante avec une précision de 15 chiffres pouvant représenter des valeurs avec une plage approximative de ± 2,23e -308 à ± 1,79e +308. **Utiliser la valeur décimale en raison du problème d’exportation tooExel** |
| Single |Représente un nombre à virgule flottante avec une précision de 7 chiffres pouvant représenter des valeurs avec une plage approximative de ± 1,18e -38 à ± 3,40e +38 |
| Guid |Représente une valeur d’identificateur unique de 16 octets (128 bits) |
| Int16 |Représente une valeur entière de 16 bits signée |
| Int32 |Représente une valeur entière de 32 bits signée |
| Int64 |Représente une valeur entière de 64 bits signée |
| String |Représente des données de type caractère à longueur fixe ou variable |

## <a name="see-also"></a>Voir aussi
* Si vous êtes intéressé par le fonctionnement hello le processus de mappage global OData et leur objectif, lisez cet article [mappage du Service de données OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview définitions, des structures et des instructions.
* Si vous souhaitez parcourir les exemples, consultez cet article [exemples de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee exemple de code et comprendre la syntaxe du code et du contexte.
* toohello tooreturn prescrit le chemin d’accès pour la publication d’un Service de données de toohello Azure Marketplace, lisez cet article [Guide de publication de Service de données](marketplace-publishing-data-service-creation.md).
