# psql

## type de donnee

* numériques : integer (smallint, bigint), real (double precision)

* dates : date (time, timestamp)

* chaînes : char, varchar

* autres : boolean

* identifiant : serial, uuid

* numériques : money

* chaînes : text

* non SQL : xml, json

## LMD

### SELECT

### Comparaison

* A = B
* A <> B
* A < B
* A > B
* A <= B
* A >= B
* A BETWEEN B1 AND B2
* A IN (B1,B2,B3....)
* A LIKE '%zhacheny%'
* A IS NULL
* OR
* NOT
* AND

### Renommage

```sql
SELECT t1.attribut1, t2.attribut2
FROM table1 t1, table2 t2
```

AS pour definir un alias

### SELECT DISTINCT（去重）

### ORDER BY（排序）
DESC ｜ ASC
默认ASC
多个比较元素 从左往右比

### Requete

#### Restriction

```sql
SELECT *
FROM R
WHERE <condition>
```

#### Projection

```sql
SELECT P1, P2, Pi
FROM R
```

#### Produit cartesien

```sql
SELECT *
FROM R1, R2, Ri
```

#### Jointure naturelle

```sql
SELECT *
FROM R1, R2, Ri
WHERE <condition>

SELECT *
FROM R1 INNER JOIN R2
ON <condition>
```

#### Jointure externe

```sql
SELECT Num
FROM Avion LEFT OUTER JOIN Vol
ON Avion.Num=Vol.Num
```
![](https://nf18.ens.utc.fr/cours/09Dsql2_web/res/exJointure.png)

    jointure naturelle

![](https://nf18.ens.utc.fr/cours/09Dsql2_web/res/exJointureExterneG.png)

    jointure externe gauche

#### Opérateurs ensemblistes

```sql
SELECT * FROM R1
UNION
SELECT * FROM R2
```

```sql
SELECT * FROM R1
INTERSECT
SELECT * FROM R2
```

```sql
SELECT * FROM R1
EXCEPT
SELECT * FROM R2
```
