
Hello série %.*ls est optimisé pour les charges de travail qui requièrent un stockage temporaire à faible latence, telles que des bases de données NoSQL Cassandra, MongoDB, Cloudera, y compris les et Redis. Hello série Ls offre jusqu'à too32 processeurs virtuels à l’aide de hello [le processeur Intel® Xeon® E5 v3 famille](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). Hello série Ls obtient hello même performances de l’UC comme hello série/GS-G et est assortie de 8 Gio de mémoire par les processeurs.  

## <a name="ls-series"></a>Série Ls

ACU : 180-240
 
| Taille          | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s  | 4    | 32   | 678   | 8              | NA / NA (0)          | 5 000 / 125                               | 2 / 4 000       | 
| Standard_L8s  | 8    | 64   | 1,388 | 16             | NA / NA (0)          | 10 000 / 250                              | 4 / 8 000  | 
| Standard_L16s | 16   | 128  | 2,807 | 32             | NA / NA (0)          | 20 000 / 500                              | 8 / 6 000 à 16000 &#8224; | 
| Standard_L32s* | 32 | 256  | 5,630 | 64             | NA / NA (0)          | 40 000 / 1 000                            | 8 / 20 000 | 
 

débit de disque maximal Hello possible avec les machines virtuelles de série %.*ls peut être limité par le nombre de hello, taille et d’entrelacements de n’importe quel des disques attachés. Pour plus d’informations, consultez l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../articles/storage/common/storage-premium-storage.md). 

* Instance est isolé toohardware tooa dédié seul client.

