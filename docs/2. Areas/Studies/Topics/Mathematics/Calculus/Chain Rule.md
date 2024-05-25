---
share: "true"
---


![[../../../../../A representation of Chain Rule from Deep Learning from Scratch - Pasted image 20231203184705.png|A representation of Chain Rule from Deep Learning from Scratch - Pasted image 20231203184705]] (Image source: [[../../../../../3. Resources/book-manual-notes/Book - Deep Learning from Scratch|Deep Learning from Scratch]] by [[@Seth Weidman|Mr Seth Weidman]])

Assume two functions $f_{1}(u) \text{ and } f_{2}(u)$. 
Consider the composite function $f(u) = f_{2}(f_{1}(u))$. 

Chain Rule mathematically states: The derivative of the composite function $f$ at a value $x$ will be the product of the derivative of $f_1$ at $x$ times the derivative of $f_2$ at $f_1(x)$:

$$\frac{df_{2}}{du}(x) = \frac{df_{2}}{du}(f_{1}(x)) \times \frac{df_{1}}{du}(x)$$

