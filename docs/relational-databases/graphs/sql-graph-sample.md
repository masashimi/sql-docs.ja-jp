---
title: SQL データベースのサンプルを Graph |Microsoft Docs
description: のに役立つ簡単なサンプルは、SQL グラフ データベースで導入された新しい構文の概要します。
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, tsql reference
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 06c6ef2876dd7e347fd969e7bdc427e4b1bc9318
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43108572"
---
# <a name="create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sql"></a>グラフ データベースを作成し、T-SQL を使用してクエリに一致するパターンはいくつかの実行
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

このサンプルでは、[!INCLUDE[tsql-md](../../includes/tsql-md.md)]ノードとエッジのグラフ データベースを作成し、新しい MATCH 句を使用して、いくつかのパターンに一致して、グラフを走査するスクリプト。 このサンプル スクリプトは Azure SQL データベースの両方で動作し、 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]  
 
## <a name="sample-schema"></a>サンプル スキーマ  
このサンプルは、人、レストラン、市区町村のノードを持つ仮想的なソーシャル ネットワークの図 1 に示すように、グラフ スキーマを作成します。 これらのノードは、友人を使用して相互に接続しているいいね!、LivesIn と LocatedIn のエッジ。 

![人の都市のレストラン テーブル](../../relational-databases/graphs/media/person-cities-restaurants-tables.png "Sql グラフ データベースのサンプル")  
レストラン、市区町村、person ノードおよび LivesIn LocatedIn、いいねの端を図 1: サンプルのスキーマです。


## <a name="sample-script"></a>サンプル スクリプト
```
-- Create a graph demo database
CREATE DATABASE graphdemo;
go

USE  graphdemo;
go

-- Create NODE tables
CREATE TABLE Person (
  ID INTEGER PRIMARY KEY, 
  name VARCHAR(100)
) AS NODE;

CREATE TABLE Restaurant (
  ID INTEGER NOT NULL, 
  name VARCHAR(100), 
  city VARCHAR(100)
) AS NODE;

CREATE TABLE City (
  ID INTEGER PRIMARY KEY, 
  name VARCHAR(100), 
  stateName VARCHAR(100)
) AS NODE;

-- Create EDGE tables. 
CREATE TABLE likes (rating INTEGER) AS EDGE;
CREATE TABLE friendOf AS EDGE;
CREATE TABLE livesIn AS EDGE;
CREATE TABLE locatedIn AS EDGE;

-- Insert data into node tables. Inserting into a node table is same as inserting into a regular table
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table, 
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 1), 
       (SELECT $node_id FROM Restaurant WHERE id = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 2), 
      (SELECT $node_id FROM Restaurant WHERE id = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 3), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 4), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 5), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 1),
      (SELECT $node_id FROM City WHERE id = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 2),
      (SELECT $node_id FROM City WHERE id = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 3),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 4),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 5),
      (SELECT $node_id FROM City WHERE id = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 1),
      (SELECT $node_id FROM City WHERE id =1));
INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 2),
      (SELECT $node_id FROM City WHERE id =2));
INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 3),
      (SELECT $node_id FROM City WHERE id =3));

-- Insert data into the friendof edge.
INSERT INTO friendof VALUES ((SELECT $NODE_ID FROM person WHERE ID = 1), (SELECT $NODE_ID FROM person WHERE ID = 2));
INSERT INTO friendof VALUES ((SELECT $NODE_ID FROM person WHERE ID = 2), (SELECT $NODE_ID FROM person WHERE ID = 3));
INSERT INTO friendof VALUES ((SELECT $NODE_ID FROM person WHERE ID = 3), (SELECT $NODE_ID FROM person WHERE ID = 1));
INSERT INTO friendof VALUES ((SELECT $NODE_ID FROM person WHERE ID = 4), (SELECT $NODE_ID FROM person WHERE ID = 2));
INSERT INTO friendof VALUES ((SELECT $NODE_ID FROM person WHERE ID = 5), (SELECT $NODE_ID FROM person WHERE ID = 4));


-- Find Restaurants that John likes
SELECT Restaurant.name
FROM Person, likes, Restaurant
WHERE MATCH (Person-(likes)->Restaurant)
AND Person.name = 'John';

-- Find Restaurants that John's friends like
SELECT Restaurant.name 
FROM Person person1, Person person2, likes, friendOf, Restaurant
WHERE MATCH(person1-(friendOf)->person2-(likes)->Restaurant)
AND person1.name='John';

-- Find people who like a restaurant in the same city they live in
SELECT Person.name
FROM Person, likes, Restaurant, livesIn, City, locatedIn
WHERE MATCH (Person-(likes)->Restaurant-(locatedIn)->City AND Person-(livesIn)->City);

```

## <a name="clean-up"></a>クリーンアップします。  
スキーマとサンプル用に作成されたデータベースをクリーンアップします。
```
USE graphdemo;
go

DROP TABLE IF EXISTS likes;
DROP TABLE IF EXISTS Person;
DROP TABLE IF EXISTS Restaurant;
DROP TABLE IF EXISTS City;
DROP TABLE IF EXISTS friendOf;
DROP TABLE IF EXISTS livesIn;
DROP TABLE IF EXISTS locatedIn;

USE master;
go
DROP DATABASE graphdemo;
go


```

## <a name="script-explanation"></a>スクリプトの説明  
このスクリプトでは、新しい T-SQL 構文を使用して、ノードとエッジ テーブルを作成します。 使用してノードとエッジ テーブルにデータを挿入する方法を示します`INSERT`ステートメントを使用する方法も示しています`MATCH`パターン マッチングとナビゲーションの句。

|コマンド    |注
|---  |---  |
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)  |グラフ ノードまたはエッジ テーブルを作成します。  |
|[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)  |ノードまたはエッジ テーブルに挿入します。  |
|[一致&#40;TRANSACT-SQL&#41;](../../t-sql/queries/match-sql-graph.md)  |一致を使用して、パターンに一致またはグラフの走査  |
