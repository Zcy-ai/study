# Contraint

## Cardinalité


![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/06a1n.png)

* Si la cardinalité est exactement 1 (1..1) côté 1, alors on ajoutera une contrainte de non nullité sur la clé étrangère

* Si la cardinalité est au moins 1 (1..N) côté N, on ajoutera une contrainte d'existence de tuples référençant pour chaque tuple de la relation référencée.

        添加一个限制保证R1中的所有元素都有被R2引用到

        R1(#a,b)

        R2(#c,d,a=>R1)

        Contraintes : R2.a NOT NULL et PROJECTION(R1,a) = PROJECTION(R2,a)

* Si la cardinalité côté 1 est 0..1 alors il peut exister la valeur NULL dans R2.a et donc la contrainte devient : 

        有可能有一个键在关联的表中没有任何引用

        PROJECTION(Classe1,a) ⊆ PROJECTION(Classe2,a)

* Si la cardinalité est au moins 1 (1..N) d'un côté et/ou de l'autre, alors des contraintes d'existence simultanée de tuples devront être ajoutées.

    Pour chaque association binaire de type M:N

    ![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/07anm0.png)

    Classe1(#a,b)

    Classe2(#c,d)

    Assoc(#a=>Classe1,#c=>Classe2)

    ![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/07anm.png)

    R1(#a,b)

    R2(#c,d)

    A(#a=>R1,#c=>R2)

    Contraintes: (R1,a) = PROJECTION(A,a) AND PROJECTION(R2,c) = PROJECTION(A,c)

    Si la cardinalité est 0..N:1..N seule une des deux contraintes est exprimée.

* 