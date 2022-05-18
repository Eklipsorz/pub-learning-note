
## 描述
根據[[@wikidataClassfulNetwork2022]]所描述的：

> In the original address definition, the most significant eight bits of the 32-bit IPv4 address was the _network number_ field which specified the particular network a host was attached to. The remaining 24 bits specified the local address, also called _rest field_(the rest of the address), which uniquely identified a host connected to that network.[[1]](https://en.wikipedia.org/wiki/Classful_network#cite_note-) This format was sufficient at a time when only a few large networks existed, such as the [ARPANET](https://en.wikipedia.org/wiki/ARPANET "ARPANET") (network number 10), and before the wide proliferation of [local area networks](https://en.wikipedia.org/wiki/Local_area_network "Local area network") (LANs). As a consequence of this architecture, the address space supported only a low number (254) of independent networks.

> Before the introduction of address classes, the only address blocks available were these large blocks which later became known as Class A networks.[[2]](https://en.wikipedia.org/wiki/Classful_network#cite_note-2) As a result, some organizations involved in the early development of the Internet received address space allocations far larger than they would ever need (16,777,216 IP addresses each!). It became clear early in the growth of the network that this would be a critical [scalability](https://en.wikipedia.org/wiki/Scalability "Scalability") limitation.


在分類定址出現之前的重點：
- 原本32bit 的IP中是8位元來定義不同的子網域，而剩下的24位元則是在子網域的獨特序號
- 換言之，會有256個子網域，每個子網域會有16777214個IP可分配
- 後來隨著業界對於區域網路的需求逐漸變大，導致原本的256個子網域恐怕會不夠用
- 另外由於每個子網域能夠分配的IP遠超於業界所需要的量，導致浪費過多的IP


衍生分類定址的主因：
- 子網域量太少
- 每個子網域給的IP遠超於業界需要

---
Status: #🌱 
Tags:
[[Network]]
Links:
References:
[[@wikidataClassfulNetwork2022]]