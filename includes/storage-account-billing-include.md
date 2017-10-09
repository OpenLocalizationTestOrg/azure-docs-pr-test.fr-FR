La facturation de l’utilisation d’Azure Storage est basée sur votre compte de stockage. Les coûts de stockage sont basées sur hello suivant facteurs : / région, type de compte, la capacité de stockage, schéma de réplication, les transactions de stockage et sortie de données.

* Région fait référence toohello de région géographique dans laquelle votre compte est basé.
* Type de compte fait référence toowhether vous utilisez un compte de stockage à usage général ou un compte de stockage d’objets Blob. Avec un compte de stockage d’objets Blob, couche d’accès aux hello détermine également le modèle de facturation hello pour le compte de hello.
* Capacité de stockage fait référence toohow beaucoup de votre unité de compte de stockage, vous utilisez des données de toostore.
* La réplication détermine le nombre de copies de vos données qui sont conservées simultanément et à quels emplacements.
* Les transactions font référence tooall lecture et écriture operations tooAzure stockage.
* Sortie de données fait référence toodata transféré à partir d’une région Azure. Lorsque les données de hello dans votre compte de stockage sont accessibles par une application qui n’est pas en cours d’exécution dans hello même région, vous êtes facturé pour la sortie de données. (Pour des services Azure, vous pouvez effectuer les étapes toogroup vos données et les services Bonjour mêmes données centres tooreduce ou éliminer les frais de sortie de données.)

Hello [tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/) page fournit des informations de tarification détaillées basées sur le type de compte, la capacité de stockage, la réplication et les transactions. Hello [détails de tarification des transferts de données](https://azure.microsoft.com/pricing/details/data-transfers/) fournit des informations de tarification détaillées pour la sortie de données. Vous pouvez utiliser hello [calculatrice de tarification Azure Storage](https://azure.microsoft.com/pricing/calculator/?scenario=data-management) toohelp évaluer les coûts.

