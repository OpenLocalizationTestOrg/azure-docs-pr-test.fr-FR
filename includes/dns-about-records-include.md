### <a name="record-names"></a>Noms d’enregistrement

Dans Azure DNS, les enregistrements sont spécifiés à l’aide de noms relatifs. A *complet* le nom de domaine (FQDN) comprend le nom de la zone hello, alors qu’un *relatif* n’est pas le cas du nom. Par exemple, hello relatif nom de l’enregistrement « www » dans la zone de hello « contoso.com » donne le nom d’enregistrement complet hello « www.contoso.com ».

Un *apex* enregistrement est un enregistrement DNS à la racine de hello (ou *apex*) d’une zone DNS. Par exemple, dans hello DNS zone « contoso.com », un enregistrement apex possède également hello, nom complet « contoso.com » (il est parfois appelé un *naked* domaine).  Par convention, hello nom relatif ' @' est utilisé toorepresent enregistrements de sommet.

### <a name="record-types"></a>Types d’enregistrements

Chaque enregistrement DNS a un nom et un type. Les enregistrements sont organisés en différents types selon les données toohello qu’ils contiennent. type le plus courant Hello est un enregistrement « A » qui mappe une adresse IPv4 de tooan nom. Un autre type courant est un enregistrement « MX », qui est mappé à un serveur de messagerie tooa nom.

le DNS Azure prend en charge tous les types d’enregistrement DNS courants, à savoir : A, AAAA, CNAME, MX, NS, PTR, SOA, SRV et TXT. Notez que les [enregistrements SPF sont représentés à l’aide d’enregistrements TXT](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Jeux d’enregistrements

Vous devez parfois toocreate plusieurs enregistrements DNS avec un nom donné et le type. Par exemple, site web de « www.contoso.com » hello est hébergé sur des adresses IP différentes. site Web de Hello deux nécessite un enregistrement pour chaque adresse IP. Voici un exemple de jeu d’enregistrements :

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

Le DNS Azure gère l’ensemble des enregistrements DNS à l’aide de *jeux d’enregistrements*. Un jeu d’enregistrements (également appelé un *ressource* enregistrer ensemble) est la collection hello des enregistrements DNS dans une zone qui ont hello même nom et de hello même type. La plupart des jeux d’enregistrements contiennent un seul enregistrement. Toutefois, les exemples comme hello une ci-dessus, dans laquelle un jeu d’enregistrements contient plus d’un enregistrement, ne sont pas rares.

Par exemple, supposons que vous avez déjà créé un enregistrement de « www » dans la zone de hello « contoso.com », qui pointe toohello IP adresse '134.170.185.46' (hello premier enregistrement ci-dessus).  toocreate hello deuxième enregistrement vous ajouteriez enregistrement existant toohello définir, plutôt que de créer un jeu d’enregistrements supplémentaire.

Hello SOA et les types d’enregistrements CNAME sont des exceptions. les normes DNS Hello n’autorisent pas plusieurs enregistrements avec le même nom pour ces types de hello, par conséquent, ces jeux d’enregistrements ne peut contenir un seul enregistrement.
