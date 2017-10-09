## <a name="what-is-blob-storage"></a>Présentation du stockage d'objets blob
Stockage d’objets Blob Azure est un service pour le stockage de grandes quantités de données d’objet non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS. Vous pouvez utiliser les données de tooexpose de stockage Blob publiquement toohello world ou les données d’application toostore en privé.

Voici quelques utilisations courantes du stockage d’objets blob :

* Service des images ou des documents directement tooa navigateur
* Stockage de fichiers pour un accès distribué
* Diffusion en continu de vidéo et d’audio
* Stockage de données pour la sauvegarde et la restauration, la récupération d’urgence et l’archivage
* Stockage des données pour l’analyse par un service local ou hébergé par Azure

## <a name="blob-service-concepts"></a>Concepts du service BLOB
Hello service Blob contient hello suivant des composants :

![Architecture d’objets blob](./media/storage-blob-concepts-include/blob1.png)

* **Compte de stockage :** tous accéder tooAzure stockage s’effectue via un compte de stockage. Ce compte de stockage peut être un **compte de stockage à usage général** ou un **compte de stockage d’objets blob** spécialisé pour le stockage des objets/blobs. Pour plus d’informations, voir [À propos des comptes de stockage Azure](../articles/storage/common/storage-create-storage-account.md).
* **Conteneur :** un conteneur regroupe un ensemble d'objets blob. Tous les objets blob doivent figurer dans un conteneur. Un compte peut contenir un nombre illimité de conteneurs. Un conteneur peut stocker un nombre illimité d’objets blob. Notez que ce nom de conteneur hello doit être en minuscule.
* **Objet blob :** fichier de tout type et de toute taille. Azure Storage propose trois types d’objets blob : les objets blob de blocs, les objets blob d’ajouts et les objets blob de pages.
  
    Les *objets blob de blocs* sont parfaits pour le stockage des fichiers texte ou binaires, tels que les documents et les fichiers multimédias. *Ajouter des objets BLOB* sont similaires tooblock BLOB dans la mesure où ils sont composés de blocs, mais ils sont optimisés pour les opérations d’ajout, afin qu’ils soient utiles pour les scénarios de journalisation. Objet blob de blocs unique peut contenir des too50, 000 blocs de too100 Mo chacun, pour une taille totale de 4,75 To légèrement supérieur à (100 Mo X 50 000). Un objet blob d’ajout unique peut contenir des too50, 000 blocs de too4 Mo chacun, pour une taille totale de légèrement supérieur à 195 Go (4 Mo X 50 000).
  
    *Objets BLOB de pages* peut être jusqu'à to too1 taille et sont plus efficaces pour les opérations de lecture/écriture fréquentes. Azure Virtual Machines utilise des objets blob de pages comme disques de données et disques du système d’exploitation.
  
    Pour plus de détails sur l’affectation de noms aux conteneurs et objets blob, consultez [Affectation de noms et références aux conteneurs, objets blob et métadonnées](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

