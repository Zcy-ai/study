# Opérateurs

## 1.Projection

une opération unaire

La projection de R1 sur une partie de ses attributs {A1,A2,...} produit une relation R2

R2 = Projection{R1, a1, a2, ...}

## 2.Restriction

La restriction de R1, étant donnée une condition C, produit une relation R2 de même schéma que R1

R2 = Restriction(R1, condition C)

## 3.Jointure

La jointure est une opération binaire (c'est à dire portant sur deux relations). 

La jointure de R1 et R2, étant donné une condition C portant sur des attributs de R1 et de R2, de même domaine, produit une relation R3 ayant pour schéma la juxtaposition de ceux des relations R1 et R2 et pour tuples l'ensemble de ceux obtenus par concaténation des tuples de R1 et de R2, et qui vérifient la condition C.

R = Jointure (R1, R2, condition)

### Type de jointure

#### Jointure naturelle

不需要写出来具体是JOIN ON哪个属性，自动根据相同的属性匹配（至少有一个属性有相同的属性名）

Soit deux relation  R1(A,B,C) et R2(A,D)

Jointure(R1,R2,R1.A=R2.A) == JointureNaturelle(R1,R2)

#### Jointure externe

Jointure会导致那些仅属于一个Relation的元组丢失

![](https://www.runoob.com/wp-content/uploads/2013/09/img_innerjoin.gif)

* Jointure externe gauche

左表的属性值全部显示，右表如果没有匹配就显示为NULL

![](https://www.runoob.com/wp-content/uploads/2013/09/img_leftjoin.gif)

* Jointure externe droit

![](https://www.runoob.com/wp-content/uploads/2013/09/img_rightjoin.gif)


## 4.Produit cartésien

une opération binaire

Le produit de R1 par R2 (équivalent au produit de R2 par R1) produit une relation R3 ayant pour schéma la juxtaposition de ceux des relations R1 et R2 et pour tuples l'ensemble des combinaisons possibles entre les tuples de R1 et ceux de R2.

R = Produit (R1, R2)

## 5.Division

## 6.Renommage

