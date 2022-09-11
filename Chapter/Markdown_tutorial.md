# Markdown Tutorial

Michael Wiest 2018

---

# Text weight

# Really heavy text!
## Less heavy
### Even littler
#### I'm shrinking
##### Oh no
###### plz help
This is some normal text...

This is a new paragraph
that continues in the same line despite the line break.


---


# Text formatting

 **I'm bold!**

 *I'm italic!*

### <span style="color:cyan">COLOR!</span> <span style="color:red">COLOR!</span> <span style="color:yellow">COLOR!</span> <span style="color:magenta">COLOR!</span>



---

# Links
## [I'm a hyperlink](https://en.wikipedia.org/wiki/YOLO_(aphorism)
[*I'm a small italic link*](https://en.wikipedia.org/wiki/YOLO_(aphorism)

___


# Quoting

"Normal Quotes"

Block quotes!

>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris a ipsum nec justo dictum convallis. Integer luctus ultricies tortor sit amet vehicula. Nam tristique faucibus pharetra. Cras nec erat ligula. Proin at odio ex. Nulla ornare imperdiet nulla, sed posuere est imperdiet et. Curabitur egestas risus vitae quam pulvinar, in vulputate leo mollis. Fusce nec tincidunt libero. Suspendisse odio urna, pretium eget lectus id, accumsan bibendum ex. Aenean accumsan malesuada sem, at blandit dui euismod a. Sed sed eros porttitor, iaculis augue id, pulvinar mi. Ut in scelerisque libero, quis malesuada sem. Donec commodo diam quis massa condimentum, non consequat orci bibendum. Praesent auctor tellus egestas felis tincidunt, eget imperdiet lorem pharetra.

---

# Pictures
Two ways to format this
![Puppy0](https://www.merriam-webster.com/assets/mw/images/article/art-wap-landing-mp-lg/puppy-3143-ad4140d8f6055cda2cd8956d4af37ea9@1x.jpg "A puppy!")


![Puppy1][puppy2]

[puppy2]: https://i.ytimg.com/vi/AZ2ZPmEfjvU/maxresdefault.jpg "Another Puppy!!"


[![Puppy2](https://pbs.twimg.com/profile_images/446566229210181632/2IeTff-V_400x400.jpeg "This puppy is a link!")](nytimes.com)

---

# Code
You can reference variables like `x` or `y` inline.
But you can also have block quotes like:
```
import numpy as np
random = np.random.randn(10, 10)

print('Hello World!')
```
But you can even format the text for languages:
```python
import numpy as np
random = np.random.randn(10, 10)

print('Hello World!')
```
**Pretty!**


----

# Lists

1. Item One
2. Another


* Unordered Item
* Another one!

---

# Tables
Note the different alignments

|Time of day| Favorite snack | Why?                |
|-----------|:----------------:|----:              |
|Morning    | Oreos!           | Delicious         |
|Afternoon  | Otter Pop        | It's hot out baby |
|Night      | IPA              | I need it. |

# Comments (look at the source code)

[comment]: <> (This is a comment
               everything in here won't be in the final doc)

 <!---
This is also a comment :)
 -->
