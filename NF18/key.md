## Key

### Definition
Une clé est un groupe d'attributs minimum qui permet de'identifier de façon univoque un tuple dans une relation.

⚠️ La cle est unique et not null

### Type

#### Clé primaire
如果很多键存在于一个relation中，则选择其中一个，将其作为Clé primaire，他是immutable（一旦赋值即不可变）和simple的
#### Clés candidates
那些未被选为主键的键称为Clés candidates

#### Clé artificielle
一个附加的属性，本身没有任何含义。仅用于作为唯一标识/简化数据库中的外键引用。在定义上与之相反的称为Clé signifiant（本身带有含义）

⚠️ 在逻辑模型层面，我们必须避免用​​人工键识别所有关系

🌟🌟🌟
* 如果存在至少一个由单个属性组成的immutable的Clé naturelle，则选择其中一个作为主键
* 否则，我们可以尝试使用多个属性组成一个tuple作为主键，这样可以大概率保证他不会重复（unicite），但存在修改其中某个值的风险，一定程度损害了immutable

#### 




