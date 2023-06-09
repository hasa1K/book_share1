# 为什么软件会退化
软件的本质就是对真实世界的模拟，每个软件都能在真实世界中找到它的影子。软件的业务逻辑如果与真实世界不一样，用户就会提交新需求和bug。在我们不断地修复 Bug，实现新需求的过程中，软件的业务逻辑也会越来越接近真实世界，使得我们的软件越来越专业，让用户感觉越来越好用。但是，在软件越来越接近真实世界的过程中，业务逻辑就会变得越来越复杂，软件规模也越来越庞大。随着软件越来越复杂，如果我们还在原有框架上添加新功能，不断塞代码，就会造成软件退化。
# 有哪些方法可以减少或者阻止软件的退化
开放-封闭原则（OCP） 分为开放原则与封闭原则两部分
1. 开放原则：我们开发的软件系统，对于功能扩展是开放的（Open for Extension），即当系统需求发生变更时，可以对软件功能进行扩展，使其满足用户新的需求。
2. 封闭原则：对软件代码的修改应当是封闭的（Close for Modification），即在修改软件的同时，不要影响到系统原有的功能，所以应当在不修改原有代码的基础上实现新的功能。也就是说，在增加新功能的时候，新代码与老代码应当隔离，不能在同一个类、同一个方法中。
应当采用两顶帽子的方式进行设计：
1. 在不添加新功能的前提下，重构代码，调整原有程序结构，以适应新功能；
2. 实现新的功能。
正确的思路就是不求过度设计，为当前需求进行设计，使其刚刚满足当前需求.
