---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
title: The Transactions Layer
---


## Purpose

The [Transactions layer](Overview#transactions) layer describes the commercial agreements that govern the exchange of goods. These exchanges include change of ownership, custody, etc.. of the goods from a legal point of view. These exchanges are not rigidly coupled to physical changes in the goods. For example goods can be bought while siting at the manufacturer's warehouse, or even before the goods even exist. Even though in Supply Chains transactions mainly refer to physical goods, this may not always be the case. The goods object of the transaction may be intangible like the performance of a service.

The base transaction is that of a Sale or Purchase. A [Sale](https://www.investopedia.com/terms/s/sale.asp) represents a change of legal owner in exchange for currency. A Purchase is just a Sale named from the point of view of the buyer instead of the seller.

Other common language transactions like *Leasing*, *Insuring*, etc. can be seen as *Sale* transactions with a different good underneath. As an example, A *Lease* transaction is a *Sale* where the underlying good is the right of use or a particular good.

## Supply Chain Activities

The Transactions layer needs to support all the activities of buying and selling goods between a *Buyer* and a *Seller* and a *Buyer*, who are entities with legal agency (able to enter into legal agreements). This includes defining and entering into an agreement between parties, fulfillment of the obligations of the agreement and accrual of the corresponding currency payment obligations. *Payments* themselves require a different set of activities in the business that manage the traditional *Accounts Receivable* and *Accounts Payable*.

## Key Concepts

From the description above, we can formulate an initial set of concepts at the center of the Transactions layer. The central concept is that of an *Order*, it could also be called a *Transaction* or a *Sale*. We find the name *Order* more desirable because it is more evocative of concrete information in the mind of most practitioners like an *Order* being composed of a set of lines, each of them describing some goods to be transacted, etc.

A *Good* is the object of the commercial exchange

## Class Model

```plantuml
@startuml (id=ORDER_CLUSTER)

!include style.ipuml
hide <<Value>> stereotype

title
= Order Entity
end title

!include Projects/scac-technology/02_supply-chain-information-structure/assets/transaction-classes.puml
remove Allocation
remove UnitOfMeasure

Fulfillment "1" --> "*" Accrual
Fulfillment "*" --> "0..*" Good
Line "*" --> "1" SKU: for

SKU "1" <- "*" Good: is described by

Order "0..*" -> Party: buyer
Order "0..*" -> Party: seller

Order "1" *--> "0..*" Line

Order "1" *--> "0..*" Fulfillment

@enduml
```

```plantuml
@startuml (id=ORDER_PREALLOCATION)

!include style.ipuml
hide <<Value>> stereotype

title
= Support Pre Allocation of goods
end title

'!include Projects/scac-technology/02_supply-chain-information-structure/assets/transaction-classes.puml
'remove Fulfillment
remove Order
remove Party
remove Accrual
remove UnitOfMeasure


Line "*" --> "1" SKU: for
SKU "1" <- "*" Good: is described by

Line "1" *-> "*" Allocation
Allocation "*" --> "0..1" Good: of

Fulfillment "*" --> "0..*" Good: with
Allocation "*" <- "1" Fulfillment: from

@enduml
```

## `<ClassXX>` Details

## References

- Investopedia Definition of Sale: [Sale](https://www.investopedia.com/terms/s/sale.asp)

</div>
