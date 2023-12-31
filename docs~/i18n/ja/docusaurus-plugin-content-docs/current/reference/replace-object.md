﻿# Replace Object

![Replace Object](replace-object.png)

Replace Objectコンポーネントを使うことで、任意のGameObjectの内容を完全に置き換えることができます。

## どんな時に使うべきか？

Replace Objectコンポーネントは、オブジェクトを別のオブジェクトに置き換えたい時に便利です。
たとえば、ベースアバターのPhysBones構成を置き換えたり、ボディメッシュを別のメッシュに置き換えたりすることができます。

## 使うべきでない時は？

オブジェクトは、複数のオブジェクトに置き換えることができません。Replace Objectを使って、
他のアセットがReplace Objectも使っている場合は競合してしまうため、互換性が損なわれることになります。

## 詳細仕様

### 子オブジェクトの扱い

Replace Objectは、指定されたオブジェクトのみを置き換えます。元のオブジェクトと置き換えオブジェクトの子オブジェクトは、
両方とも置き換えオブジェクトの下に配置されます。

### オブジェクト名

Replace Objectは、置き換えオブジェクトの名前を変更しません。そのため、置き換えオブジェクトの名前が元のオブジェクトと異なる場合、
最終的なオブジェクト名も異なることになります。ただし、Replace Objectは、元のオブジェクトを参照するアニメーションパスを、
置き換えオブジェクトを参照するように更新します。

Replace Objectは、アバター処理の最後のほうに実行されるため、ほとんどの場合はあまり問題になりません。ただし、
ボディメッシュを置き換えてMMD互換性を維持したい場合などは、問題になる可能性があります。逆に、既存のアバターにMMD互換性を追加したい場合はこの
仕様をあえて応用することもできます。

### コンポーネント参照の扱い

Replace Objectは、古いオブジェクトのコンポーネントへの参照を、新しいオブジェクトへの参照に置き換えようとします。
古いオブジェクトに同じコンポーネントが複数ある場合、参照は新しいオブジェクトの同型内で同じ順番のコンポーネントに置き換えます。
（もし新しいオブジェクトに同じコンポーネントが足りない場合は、参照はnullになります。）

Replace Objectは、曖昧なマッチングは行いません。たとえば、Box ColliderをSphere Colliderに置き換えた場合、
古いBox Colliderへの参照はnullになります。