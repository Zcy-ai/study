## Héritage

### Definition
L'héritage est l'association entre deux classes permettant d'exprimer que l'une est plus générale que l'autre. L'héritage implique une transmission automatique des propriétés (attributs et méthodes) d'une classe A à une classe A'.
Dire que A' hérite de A équivaut à dire que A' est une sous-classe de A. On peut également dire que A est une généralisation de A' et que A' est une spécialisation de A.

儿子继承妈妈的所有Method、attribut、association

Factorisation
![avatar](https://nf18.ens.utc.fr/cours/05Cmod2-heritage_web/res/heritageFact.png)

Is-a
如果c类有一个和A类的association，A的儿子B也与C有association
![avatar](https://nf18.ens.utc.fr/cours/05Cmod2-heritage_web/res/heritageIsa.png)

### Classe abstraite
Une classe abstraite est une classe <strong>non instanciable</strong>. Elle exprime donc une généralisation abstraite, qui ne correspond à aucun objet existant du monde

抽象类用斜体表示 <em>classe abstraite</em>或者用抽象的英文标注出它是抽象类
抽象类是用于被继承的，它可以被一个抽象类继承虽然一般没卵用
### Type d'heritage

#### Héritage complet
Un héritage est complet si ses classes filles n'ont aucune caractéristiques (attributs, méthodes, associations) propres.
![avatar](https://nf18.ens.utc.fr/cours/05Cmod2-heritage_web/res/14h_c0.png)

#### Héritage exclusif
Un héritage est exclusif si les objets d'une classe fille ne peuvent appartenir aussi à une autre classe fille. On peut le noter avec la contrainte {X} sur le diagramme UML ({XT} si la classe mère est abstraite).
一个对象要么是classe2要么是classe3
![avatar](https://nf18.ens.utc.fr/cours/05Cmod2-heritage_web/res/14h_x0.png)

我们尽可能使用Héritage exclusif（无论在解释还是机器实现方面）

#### Héritage multiple
L'héritage multiple est une forme d'héritage qui exprime qu'une classe fille hérite de plusieurs classes mères.

避免使用，一个多重继承可以用几个简单继承来代替

#### Héritage par référence(des filles vers la mère)
La clé primaire de la classe mère est utilisée pour identifier chacune de ses classes filles : cette clé étant pour chaque classe fille à la fois la clé primaire et une clé étrangère vers la classe mère.
子类有一个主键指向父类的外键
![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/14h0.png)
Classe1(#a,b)
Classe2(#a=>Classe1,c,d) avec c KEY
Classe3(#a=>Classe1,e,f) avec e KEY

#### Héritage par une référence et vues
![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/14h0.png)
Classe1(#a,b)
Classe2(#a=>Classe1,c,d) avec c KEY
Classe3(#a=>Classe1,e,f) avec e KEY
vClasse2=jointure(Classe1,Classe2,a=a)
vClasse3=jointure(Classe1,Classe3,a=a)

#### Héritage par référence(de la mère vers les filles)
![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/14h0.png)
La classe mère référence chacune de ses classes filles
Classe1(#a,b,c=>Classe2, e=>Classe3) avec c UNIQUE et e UNIQUE
Classe2(#c,d)
Classe3(#e,f)

#### Héritage par les classes filles
![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/14h_a0.png)
* 当父类是抽象类时
R2(#a,b,c,d) avec c KEY
R3(#a,b,e,f) avec e KEY
Contraintes : INTERSECTION (PROJECTION(R2,a), PROJECTION(R3,a)) = {}
* 当父类不是抽象类时
R1(#a,b)
R2(#a,b,c,d) avec c KEY
R3(#a,b,e,f) avec e KEY
Contraintes :
INTERSECTION (PROJECTION(R2,a), PROJECTION(R3,a)) = {}
INTERSECTION (PROJECTION(R1,a), (PROJECTION(R2,a) UNION PROJECTION(R3,a)) = {}

#### Héritage par la classe mère
* non complet

![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/14h_apc.png)

R1(#a,b,c,d,e,f,t:{2,3})
Contraintes :
t NOT NULL
NOT (t=2 AND f)
NOT (t=3 AND d)
t=2 AND d (si d est non nul)
t=3 AND f (si f est non nul)

* Héritage par la classe mère avec classe mère abstraite

![](https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/14h_a0.png)

R1(#a,b,c,d,e,f,t:{2,3})

Contraintes :
t NOT NULL
c UNIQUE
e UNIQUE
t=2 AND c
t=3 AND e
NOT (t=2 AND (e OR f)
NOT (t=3 AND (c OR d)


### Équivalence entre association d'héritage et association 1:1
![](https://nf18.ens.utc.fr/cours/05Cmod2-heritage_web/res/heritage-cardinalites.png)


### Contraintes

#### Héritage par référence
https://nf18.ens.utc.fr/cours/12Cmod3-contraintes_web/res/14h0.png