---
title: "aaaGuide toocreating un Service de données pour hello Marketplace | Documents Microsoft"
description: "Comment toocreate, certifier et déployer un Service de données pour obtenir des instructions détaillées d’achat sur hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Mappage d’un tooOData de service web existant via CSDL
> [!IMPORTANT]
> **À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.** Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners). Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Cet article donne une vue d’ensemble sur la façon de toouse un toomap CSDL un tooan de service service compatible OData existante. Il explique comment toocreate hello document de mappage (CSDL) qui transforme la demande d’entrée hello client de hello via un appel de service et un hello sortie client de toohello (données) via un flux compatible OData. Microsoft Azure Marketplace expose les utilisateurs finaux toohello de services à l’aide du protocole OData de hello. L’exposition des services par les fournisseurs de contenu (les propriétaires de données) s’effectue sous diverses formes, telles que REST, SOAP, etc.

## <a name="what-is-a-csdl-and-its-structure"></a>Qu’est un langage CSDL et sa structure ?
Un langage CSDL (Conceptual Schema Definition Language) est une spécification définissant comment toodescribe web service ou une base de données de service en commun XML est affecté toohello Azure Marketplace.

Vue d’ensemble simple de hello **flux de demande :**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Hello **flux de données** est Bonjour opposé direction :

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Figure 1** diagrammes comment un client serait obtenir des données à partir d’un fournisseur de contenu (votre service) en accédant via hello Azure Marketplace.  Hello CSDL est utilisé à la demande de hello mappage/la Transformation composant toohandle hello et passer des données entre hello demande du client et des services du fournisseur de contenu hello.

*Figure 1 : Le flux détaillé émanant du fournisseur de toocontent client via Azure Marketplace*

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Pour plus d’informations sur le protocole OData de hello lors de quelle version des extensions Azure Marketplace hello Atom et Atom Pub, passez en revue : [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

Extrait supérieure lien : *« hello hello Open Data protocol (OData visés ci-après tooas) vise protocole tooprovide basé sur un REST pour les opérations CRUD-style (création, lecture, mise à jour et suppression) sur les ressources exposées en tant que services de données. Un « service de données » est un point de terminaison où des données sont exposées à partir d’une ou de plusieurs « collections », chacune comportant zéro « entrées » ou plus, qui consistent en des paires nom-valeur typées. OData est publié par Microsoft sous les Standards OASIS (Organization for hello for the Advancement of Structured Information Standards) afin que toute personne qui souhaite toocan générer des serveurs, des clients ou des outils sans les droits d’auteur ou restrictions. »*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Trois éléments critiques qui ont toobe défini par hello CSDL sont :
* Hello **point de terminaison** de fournisseur de services de hello hello Web adresse (URI) de hello Service
* Hello **des paramètres de données** passé en tant que fournisseur de services de toohello d’entrée des définitions de hello des paramètres de hello envoyés service du fournisseur de contenu toohello toohello les type de données.
* **Schéma** de schéma de hello toohello demandant un Service de données hello remises en service du fournisseur de contenu hello de renvoi des données hello, y compris les types de conteneur, les collections et les tables, les variables ou des colonnes et les données.

Hello suivant schéma montre une vue d’ensemble du flux de hello d’où client de hello entre hello OData instruction (service web de l’appel toohello du fournisseur du contenu) toogetting hello résultats/stockage des données.

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>Étapes :
1. Client envoie la demande via l’appel de Service terminée avec des paramètres d’entrée définis dans XML toohello Azure Marketplace
2. CSDL est utilisé toovalidate hello appel de Service.
   * Hello mis en forme un appel de Service est ensuite envoyé toohello Service de fournisseurs de contenu en hello Azure Marketplace
3. exécute Hello Webservice et valide l’action hello Hello verbe Http (c'est-à-dire GET) les données de salutation sont retournées tooAzure Marketplace où hello demande des données (le cas échéant) est présente dans un Format XML toohello Client à l’aide de hello mappage défini dans hello CSDL.
4. Hello Client reçoit les données de salutation (le cas échéant) au format XML ou JSON

## <a name="definitions"></a>Définitions
### <a name="odata-atom-pub"></a>ATOM Pub OData
ATOM pub d’un toohello extension où chaque entrée représente une ligne d’un résultat défini. Hello contenu partie entrée de hello est toocontain améliorée des valeurs de hello de ligne de hello – en tant que paires clé-valeur. Vous trouverez des informations supplémentaires ici : [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL (Conceptual Schema Definition Language)
Permet de définir des fonctions (SPROC) et des entités qui sont exposées via une base de données. Vous trouverez des informations supplémentaires ici : [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Cliquez sur hello **autres versions** liste déroulante et sélectionnez une version, si vous ne voyez pas l’article de hello.
> 
> 

### <a name="edm---entry-data-model"></a>EDM (Entry Data Model)
* Vue d’ensemble : [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Aperçu : [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Types de données : [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

Hello Voici hello détaillé tooRight gauche d’où client de hello entre hello OData instruction (service web de l’appel toohello du fournisseur du contenu) toogetting hello résultats/stockage des données :

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>Concepts de base du langage CSDL
Un langage CSDL (Conceptual Schema Definition Language) est une spécification définissant comment toodescribe web service ou une base de données de service en commun XML est affecté toohello Azure Marketplace. Décrit les CSDL hello critiques pièces qui **permet la transmission hello de données à partir de la Source de données de hello toohello Azure Marketplace.** les parties principales Hello sont décrits ici :

* Des informations d’interface qui décrivent toutes les fonctions disponibles publiquement (nœud FunctionImport)
* Des informations de type de données pour toutes les requêtes de messages (entrée) et réponses aux messages (sorties) (nœuds EntityContainer/EntitySet/EntityType)
* Informations sur les toobe de protocole de transport hello de liaison utilisé (en-tête de nœud)
* Informations d’adresse pour la localisation hello spécifié service (attribut BaseURI)

En bref, hello CSDL représente un contrat de plateforme - et indépendants du langage entre le demandeur de service hello et fournisseur de services hello. À l’aide de hello CSDL, un client peut localiser un service de base de données de service/web et appeler ses fonctions publiquement disponibles.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>Concernant une base de données de tooa CSDL ou d’une Collection
**Hello spécification CSDL**

CSDL est une grammaire XML utilisée pour décrire un service web. spécification de Hello proprement dite est divisée en 4 éléments principaux : EntitySet, FunctionImport ; Espace de noms et EntityType.

toomake cette toounderstand plus facile d’abstraction permet de lier une table de tooa CSDL.

N’oubliez pas les points suivants :

  CSDL représente un contrat de plateforme - et indépendants du langage entre hello **demandeur de service** et hello **fournisseur de services**. Le langage CSDL permet à un **client** de localiser un **service web/service de base de données** et d’appeler n’importe laquelle de ses **fonctions** disponibles publiquement.

Un Bonjour du Service de données pour les quatre parties d’un langage CSDL peuvent être considérés en termes de base de données, de Table, d’une colonne et d’une procédure stockée.

Mise en relation de ces éléments comme suit pour un service de données :

* EntityContainer ~= Base de données
* EntitySet ~= Table
* EntityType ~= Colonnes
* FunctionImport ~= Procédure stockée

**Verbes HTTP autorisés**

* GET-renvoie les valeurs à partir de la base de données hello (retourne une Collection)
* VALIDER – utilisé toopass tooand facultatif retour valeurs de données de base de données hello (créer une nouvelle entrée dans la collection hello, URI d’id/retour)
* Supprimer : supprime des données à partir de hello DB (supprime une collection)
* PUT - met à jour les données dans une base de données (remplace ou crée une collection)

## <a name="metadatamapping-document"></a>Document de métadonnées/de mappage
document de métadonnées/mappage Hello est utilisé toomap web existant du contenu d’un fournisseur de services afin qu’il peut être exposé comme un service web OData par système d’Azure Marketplace hello. Il est basé sur le langage CSDL et implémente quelques extensions tooCSDL tooaccommodate hello aux besoins de REST en fonction des services web exposés via Azure Marketplace. extensions de Hello sont trouvent dans hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) espace de noms.

Voici un exemple de hello CSDL : (copier et coller hello exemple CSDL dans un éditeur XML ci-dessous et modifiez toomatch votre Service.  Puis collez dans CSDL mappage sous l’onglet de DataService lors de la création de votre service Bonjour [portail de publication Azure Marketplace](https://publish.windowsazure.com)).

**Termes du contrat :** toohello des termes du contrat relatif hello CSDL [portail de publication](https://publish.windowsazure.com) les termes du contrat de l’interface utilisateur (PPUI).

* Offrent « Title » Bonjour PPUI rapporte tooMyWebOffer
* MyCompany Bonjour PPUI se rapporte trop**nom de l’éditeur** Bonjour [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) l’interface utilisateur
* Votre API rapporte tooa Web ou un Service de données (il s’agit d’un Plan Bonjour PPUI)

**Hiérarchie :** une entreprise (fournisseur de contenu) possède une ou plusieurs offres qui comprennent des plans, c’est-à-dire des services, qui sont associés à une API.

### <a name="webservice-csdl-example"></a>Exemple de service web CSDL
Se connecte tooa service qui expose un point de terminaison web application (par exemple, une application c#)

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> Afficher plus d’exemples de Service Web de CSDL dans l’article de hello [exemples de mappage existant web tooOData service via CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>Exemple de service de données CSDL
Se connecte tooa service qui expose une table de base de données ou une vue comme un point de terminaison exemple ci-dessous montre deux Qu'api pour la base de données en fonction de CSDL API (il peut utiliser des vues plutôt que des tables).

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a>Voir aussi
* Si vous êtes intéressé par apprentissage et comprendre les nœuds spécifiques hello et leurs paramètres, lisez cet article [nœuds de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour les définitions et des explications, des exemples et contexte de cas d’utilisation.
* Si vous souhaitez parcourir les exemples, consultez cet article [exemples de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee exemple de code et comprendre la syntaxe du code et du contexte.
* toohello tooreturn prescrit le chemin d’accès pour la publication d’un Service de données de toohello Azure Marketplace, lisez cet article [Guide de publication de Service de données](marketplace-publishing-data-service-creation.md).

