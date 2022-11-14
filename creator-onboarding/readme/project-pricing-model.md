---
order: 850
description: Art Blocks Project Pricing Model
---
# Project Pricing Model

This resource defines Art Blocks project pricing model. This resource is intended for artists as they are determining their project's series size and price per token. 

---

Art Blocks has imposed overall total value limitations to each release. You are not required (or even encouraged) to consume the project category's entire total value. This resource is intended for artists to better understand the relationship between project size and price per token.

Projects are in two product categories: Art Blocks Presents and Curated. Each collection is assigned a maximum resting value guided by the collection size. The maximum resting value is the total value that a project can generate at its resting price. This is calculated by multiplying the series size by the resting price. For Dutch auctions, the resting price is the final price tier of the auction sequence. For fixed-price sales, the resting price is equivalent to the fixed price. 


# Project Pricing Model Explained

The project categories are as follows:
* First Factory = an artist's first factory project on Art Blocks
* Factory Return = an artist's subsequent factory project
* Playground = a Curated artist's subsequent project
* Curated = a project released in our Curated Collection

Below is a table reference for total resting value assignable to each project type and category. 

First Factory: 40 ETH | Factory Return: 60 ETH | Playground: 80 ETH | Curated: 100 ETH

When determining overall series size and mint price, think of a sliding scale. On one side, there is the series size and on the other side there is the resting price. The smaller your collection, the larger your resting price can be and vice versa. The charts below indicate the range of options you would have in series size and resting price for each category’s maximum resting value.

# <img width="1189" alt="Screen Shot 2022-02-25 at 8 32 36 PM" src="https://user-images.githubusercontent.com/94644409/155823638-0212faaa-fdb6-4733-8b85-5663f8bea7a2.png">

Examples all with a maximum resting value of 60 ETH (Factory Return):
* 400 outputs sold via dutch auction tiers 1 > 0.5 > 0.35 > 0.22 > 0.15 (400 x 0.15 = 60)
* 250 outputs sold at a fixed price of 0.24 (250 x 0.24 = 60)
* 1000 outputs sold via dutch auction tiers 0.4 > 0.28 > 0.16 > 0.1 > 0.06 (1000 x 0.06 = 60)

_Do note that this price structure does not affect the establishment of dutch auction starting price and tiers. Artists can design their dutch auction tiers as they'd like. Artists are also not limited to the series size options outlined in the above chart._

# How To Use This Pricing Model

The above category prices impose limits on project's overall resting value. That said, you are encouraged to also consider your audience and breadth of your project/mints when determining the best series size and price per token for your project. 

Approaching price in terms of overall value leaves room for artists to ensure that their collection size and output pricing aligns with their created project. Keep in mind that if a collection uses a dutch auction sales mechanic, the collection may realize a greater value than the resting price. This pricing guidance does not limit the overall value a project may generate, it just requires that the project's resting value is not higher than these maximum prices. Conversely, artists are welcome to set prices and series sizes that fall below the specified maximum resting values. We recognize that the market is forever changing. Art Blocks will continue to monitor sales data and adjust these values as appropriate over time. 

# Price Reductions

A project's pricing cannot be altered after release. Instead, you may reduce your project size but must run the change by the Art Blocks Art Team in your [M_] DM on Discord. We recommend waiting at least 4 weeks before reducing collection size. 

Our contract automatically locks projects FOUR WEEKS after their final mint.

**Note**: If the artist reduces maxInvocations to current invocations, that tx is considered the start of the four-week timer until lock.


