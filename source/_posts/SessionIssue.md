---
title: Session Issue On a .NET website
date: 2019-03-19 10:10:15
tags:
---

Recently I solve a quite deep hidden issue on my .Net website, my colleague Tim found that he created two order for two different person, but finally the product(Order Detail part in the system ) belongs to the older order. 

I check the database, and I could see all the order details are bundled with older order header, that is the reason, but how this happen.

I check the code and take a walk through the adminarea page CartDetail and NewOrderDetail, here two import funtion is saveCart and saveOrder, but I think that issue is impossible to happen here, since when you save shopping cart in admin area, saveCart will get a new guid, and get shopping cart item from purchaser's id, if there are any existed item in the cart, it will use the guid in the existed cart, in this case, it is impossile for you to create a new item in the shoping cart that will be attached to another people's order header since here you could always select the item from purchaser id. Then I see a suspicious filed named GUID, since it is impossbile for the different order details attach to a order header if you use purchaser's Id as the key to search the order header, the only possbile issue is that we search by GUID.

Then I check the GUID of two order header and find out they are the same, so finally we find out the casue. 

But how does this happen? If we do that in admin area, it is impossible that happens. 

Then I ask my colleague Tim and find out he adds the item to shopping cart from client side and then goes to the adminarea to deal with the shopping cart, so that is how the magic happens. Since from Client side, we read the GUID from session, and if you only ad the item to the shopping cart, the GUID will not change. It will not affect the normal customer though.

