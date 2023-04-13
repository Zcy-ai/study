# Association

## Agrégation

L'agrégation est une association particulière utilisée pour préciser une relation tout/partie (ou ensemble/élément), on parle d'association méréologique.

整体和部分的关系

Les associations de type agrégation se traitent de la même façon que les associations classiques.

聚合和一般的关联处理方式是一样的

![](https://nf18.ens.utc.fr/cours/14Cmod5-assoc_web/res/12agr.png)

    Agrégation 1:N

    Classe1(#a,b)

    Classe2(#c,d,a=>Classe1)

![](https://nf18.ens.utc.fr/cours/14Cmod5-assoc_web/res/12agrnm.png)

    Agrégation N:M

    Classe1(#a,b)

    Classe2(#c,d)

    Assoc(#a=>Classe1,#c=>Classe2)

## Association

![](https://nf18.ens.utc.fr/cours/14Cmod5-assoc_web/res/assocRole.png)

    Rôle et sens de lecture sur une association

![](https://nf18.ens.utc.fr/cours/14Cmod5-assoc_web/res/reflexive.png)

    Association réflexive
    如果想添加自己不能与自身关联，可以在UML中添加约束{les personnes ne se marient pas avec elles-mêmes}或者用SQL pk != fk

## Classe d'association

On souhaite ajouter des propriétés à une association.

![](https://nf18.ens.utc.fr/cours/14Cmod5-assoc_web/res/classeassociationEx.jpg)

    Société(...)

    Personne(...)

    Emploi(#personne=>Personne, #societe=>Societe, poste:string, salaire:integer, quotite:numeric(1,2)) 

取消plusieurs emplois dans une même société的限制可以使用<strong>local key</strong>

![](https://nf18.ens.utc.fr/cours/14Cmod5-assoc_web/res/classeassociationEx-localkey.jpg)

    Société(...)
    
    Personne(...)

    Emploi(#personne=>Personne, #societe=>Societe, #poste:string, salaire:integer, quotite:numeric(7,2)) 

![](https://nf18.ens.utc.fr/cours/14Cmod5-assoc_web/res/11cla_ass20.png)

    Classe assocation (N:M)

    Classe1(#a,b)

    Classe2(#c,d)

    Assoc(#a=>Classe1,#c=>Classe2,#e,f)

