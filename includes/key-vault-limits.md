Transactions de clé (transactions maximales autorisées dans les 10 secondes, par coffre par région<sup>1</sup>) :

|Type de clé|Clé HSM<br>Clé CREATE|Clé HSM<br>Toutes les autres transactions|Clé logicielle<br>Clé CREATE|Clé logicielle<br>Toutes les autres transactions|
|:---|---:|---:|---:|---:|
|RSA 2 048 bits|5|1 000|10|2000|
|RSA 3 072 bits|5|250|10|500|
|RSA 4 096 bits|5|125|10|250|
|

Secrets, clés de compte de stockage géré et transactions de coffre :
| Type de transaction | Transactions maximales autorisées dans les 10 secondes, par coffre par région<sup>1</sup> |
| --- | --- |
| Toutes les transactions |2000 |
|

<sup>1</sup> La limite d’abonnement pour tous les types de transaction est fixée à 5x par limite de coffre de clés. Par exemple, HSM - autres transactions par abonnement sont limitées too5000 dans 10 secondes par abonnement.
