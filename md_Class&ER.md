### クラス図

#### クラス間の関係
```plantuml
@startuml
hide empty members

Student  -- Instructor    : 関連\n（association）
Car    o-- Wheel     : 集約\n（aggregation）
Car    o-- Engine
Engine_Inspection    o-- Engine
Person  *-- Head     : コンポジション\n（composition）
Person  *-- Hand     

@enduml
```

##### Association vs Aggregation vs Composition
Aggregation and Composition are subsets of association meaning they are specific cases of association. In both aggregation and composition object of one class "owns" object of another class. But there is a subtle difference:

Aggregation implies a relationship where the child can exist independently of the parent. Example: Class (parent) and Student (child). Delete the Class and the Students still exist.

Composition implies a relationship where the child cannot exist independent of the parent. Example: House (parent) and Room (child). Rooms don't exist separate to a House.

####
```plantuml
@startuml
hide empty members

ホイール ^.. タイヤ       : 依存\n（dependency）
HashMap ^-- LinkedHashMap : 汎化\n（generalization）\n\n※Java の extends
List    ^.. ArrayList     : 実現\n（realization）\n\n※Java の implements

interface List

@enduml
```
依存とは、片方のインスタンスを変更すればもう片方のインスタンスに変更が生じることを表す。

#### カーディナリティ
```plantuml
@startuml
hide circles
hide empty members

クラスA "1" ---   "1"      クラスB
クラスC "1" ---|| "only 1" クラスD
クラスE "1" ---o| "0..1"   クラスF
クラスG "1" ---|{ "1..*"   クラスH
クラスI "1" ---o{ "0..*"   クラスJ

@enduml
```

#### クラス図
~~~plantuml
@startuml

abstract class AbstractList
abstract AbstractCollection
interface List
interface Collection

List <|-- AbstractList
Collection <|-- AbstractCollection

Collection <|- List
AbstractCollection <|- AbstractList
AbstractList <|-- ArrayList

class ArrayList {
  Object[] elementData
  size()
}

enum TimeUnit {
  DAYS
  HOURS
  MINUTES
}

annotation SuppressWarnings

@enduml
~~~


#### ER図
```plantuml
@startuml
@startuml

' hide the spot
hide circle

' avoid problems with angled crows feet
skinparam linetype ortho

entity "Entity01" as e01 {
  *e1_id : number <<generated>>
  --
  *name : text
  description : text
}

entity "Entity02" as e02 {
  *e2_id : number <<generated>>
  --
  *e1_id : number <<FK>>
  other_details : text
}

entity "Entity03" as e03 {
  *e3_id : number <<generated>>
  --
  e1_id : number <<FK>>
  other_details : text
}

e01 ||..o{ e02
e01 |o..o{ e03

@enduml

@enduml
```