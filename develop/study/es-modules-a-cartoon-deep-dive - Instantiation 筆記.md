## 描述

> Like I mentioned before, an instance combines code with state. That state lives in memory, so the instantiation step is all about wiring things up to memory.

> First, the JS engine creates a module environment record. This manages the variables for the module record. Then it finds boxes in memory for all of the exports. The module environment record will keep track of which box in memory is associated with each export.

> These boxes in memory won’t get their values yet. It’s only after evaluation that their actual values will be filled in. There is one caveat to this rule: any exported function declarations are initialized during this phase. This makes things easier for evaluation.

> To instantiate the module graph, the engine will do what’s called a depth first post-order traversal. This means it will go down to the bottom of the graph — to the dependencies at the bottom that don’t depend on anything else — and set up their exports.



> The engine finishes wiring up all of the exports below a module — all of the exports that the module depends on. Then it comes back up a level to wire up the imports from that module.

> Note that both the export and the import point to the same location in memory. Wiring up the exports first guarantees that all of the imports can be connected to matching exports.


![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_01-768x316.png)

> The engine finishes wiring up all of the exports below a module — all of the exports that the module depends on. Then it comes back up a level to wire up the imports from that module.

> Note that both the export and the import point to the same location in memory. Wiring up the exports first guarantees that all of the imports can be connected to matching exports.


在實例化的過程中，會讓所有export所指定的識別字與記憶體區塊做一個對應關係，同時間也會讓import的識別字所對應的記憶體區塊也和export所對應的一樣，確保兩者都能使用相同的記憶體區塊



![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_02-768x316.png)

> This is different from CommonJS modules. In CommonJS, the entire export object is copied on export. This means that any values (like numbers) that are exported are copies.

> This means that if the exporting module changes that value later, the importing module doesn’t see that change.


![](https://hacks.mozilla.org/files/2018/03/31_cjs_variable-768x174.png)

> In contrast, ES modules use something called live bindings. Both modules point to the same location in memory. This means that when the exporting module changes a value, that change will show up in the importing module.

> Modules that export values can change those values at any time, but importing modules cannot change the values of their imports. That being said, if a module imports an object, it can change property values that are on that object.

相對來說，ES 模組會使用live bindings技術來讓模組間的export和import都指向同個記憶體區塊，這表示只要在模組上更改值，就會使用import的那一方拿到變更後的值，但import不能夠更改import識別字上的對應實體物件(記憶體內容)，最多只能增加屬性至物件上。

![](https://hacks.mozilla.org/files/2018/03/30_live_bindings_04-768x316.png)

> The reason to have live bindings like this is then you can wire up all of the modules without running any code. This helps with evaluation when you have cyclic dependencies, as I’ll explain below.

## 複習


---
Status: 
Tags:
Links:
References: