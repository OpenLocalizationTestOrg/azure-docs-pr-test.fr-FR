## <a name="what-is-table-storage"></a>Qu’est-ce qu’un stockage de table ?
Le stockage de table Azure permet de stocker de grandes quantités de données structurées. service de Hello est une banque de données NoSQL qui accepte authentifié d’appels à partir de l’intérieur et extérieur hello cloud Azure. Les tables Azure sont idéales pour le stockage des données structurées non relationnelles. Voici quelques utilisations courantes du stockage de table :

* Stockage des téraoctets de données structurées capables de servir des applications Web
* Stockage des jeux de données ne nécessitant pas de jonctions complexes, de clés étrangères ou de procédures stockées, et pouvant être dénormalisés pour un accès rapide
* Interrogation rapide des données par requête à l’aide d’un index cluster
* L’accès aux données à l’aide de protocole OData de hello et les requêtes LINQ avec les bibliothèques .NET de Service de données WCF

Vous pouvez utiliser la Table toostore et requête énormes jeux de stockage des données structurées et non relationnelles, et vos tables d’évoluera la demande croissante.

## <a name="table-storage-concepts"></a>Concepts de stockage de table
Stockage de table contient hello suivant des composants :

![Diagramme des composants du stockage de table][Table1]

* **Format d'URL :** le code traite les tables dans un compte à l'aide de ce format d'adresse :   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  Vous pouvez adresser des tables Azure directement à l’aide de cette adresse par hello protocole OData. Pour plus d’informations, consultez [OData.org][OData.org].
* **Compte de stockage :** tous accéder tooAzure stockage s’effectue via un compte de stockage. Pour plus d’informations sur la capacité du compte de stockage, consultez la page [Objectifs de performance et évolutivité du stockage Azure](../articles/storage/common/storage-scalability-targets.md) .
* **Table**: une table est une collection d’entités. Les tables n’appliquent pas de schéma sur les entités, ce qui signifie qu’une seule table peut contenir des entités ayant différents ensembles de propriétés. nombre de Hello des tables un compte de stockage peut contenir est limité uniquement par la limite de capacité de compte de stockage hello.
* **Entité**: une entité est un ensemble de propriétés, la ligne de base de données tooa similaire. Une entité peut être up too1MB taille.
* **Propriété**: une propriété est une paire nom-valeur. Chaque entité peut inclure des données de toostore too252 propriétés. Chaque entité dispose également de trois propriétés système qui spécifient une clé de partition, une clé de ligne et un horodatage. Entités avec la même clé de partition peut être interrogé plus rapidement et insérées/mises à jour dans des opérations atomiques de hello. La clé de ligne d'une entité est son identificateur unique à l'intérieur d'une partition.

Pour plus d’informations sur les tables et les propriétés d’affectation de noms, consultez [hello de présentation des modèle de données de Service de Table](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
