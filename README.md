<h1 dir="rtl">چگونه می توان شمارنده را در پایتون پیاده سازی کرد؟</h1>
<br>
<p dir="rtl">تا قبل از منتشر شدن نسخه پایتون ۳.۴ ، زبان پایتون پیاده سازی برای شمارنده ارائه نکرده بود. برنامه نویسان برای استفاده از شمارنده یا خود آن ها با توجه به نیازی که داشتند، پیاده سازی خاصی از شمارنده را انجام می دادند و از آن استفاده می کردند یا از کتاب‌خانه های آماده که بقیه برنامه نویسان آن ها را آماده و عرضه کرده بودند استفاده می کردند. از نسخه پایتون ۳.۴ شمارنده به پایتون اضافه شد و سپس به نسخه های قبلی پایتون نیز اضافه شد ولی ما برای بهره بردن از امکانات بیشتر همچنان چگونگی استفاده از شمارنده و پیاده سازی دستی آن مورد توجه است که ما به بررسی چند مورد از آن ها می پردازیم.</p>

<p dir="rtl">یک روش استفاده از شمارنده استفاده از کتاب‌خانه های آماده است که دیگر برنامه نویسان آن‌ها را آماده کرده‌اند که قابلیت های بیشتری دارند. می توان به کتابخانه های aenum و enum34 اشاره کرد. enum34 نسبت به دو نسخه پایتون ۳ و پایتون ۲ سازگار نیست برای همین استفاده از aenum توصیه می شود. برای نصب این دو کتابخانه به روش زیر عمل می کنیم: </p>

- **$ pip install aenum**
- **$ pip install enum34**

<p dir="rtl">در قطعه کد زیر نحوه استفاده از دو کتابخانه بالا توضیح داده شده است.</p>

```markdown
from aenum import Enum  # for the aenum version

Animal = Enum('Animal', 'ant bee cat dog')
Animal.ant  # returns <Animal.ant: 1>
Animal['ant']  # returns <Animal.ant: 1> (string lookup)
Animal.ant.name  # returns 'ant' (inverse lookup)
```

<p dir="rtl">یا به طور مشابه می توان مانند قطعه کد زیر عمل کرد که مانند کد بالا عمل می کند.</p>

```markdown
class Animal(Enum):
    ant = 1
    bee = 2
    cat = 3
    dog = 4
```

<p dir="rtl">یک روش ساده پیاده سازی دستی شمارنده به شکل زیر است که در آن اعضای شمارنده به عنوان آرگومان به تابع پاس داده می شود و به ترتیبی که آن ها به تابع پاس داده شده اند به آن ها مقدار داده می‌شود. </p>

```markdown
def enum(*sequential, **named):
    enums = dict(zip(sequential, range(len(sequential))), **named)
    return type('Enum', (), enums)
```
<p dir="rtl">و روش استفاده از آن هم به شکل زیر است</p>

```markdown
>>> Numbers = enum('ZERO', 'ONE', 'TWO')
>>> Numbers.ZERO
0
>>> Numbers.ONE
1
```

<p dir="rtl">روش پر کاربرد دیگری که می توان از آن برای پیاده سازی شمارنده استفاده کرد به شکل زیر است:</p>

```markdown
class Color:
    RED = 1
    BLUE = 2

x = Color.RED
```

<p dir="rtl">در این روش به دلیل این‌که شمارنده به صورت یک کلاس پیاده سازی شده است می توان ویژگی ها آن را تغییر داد و با توجه به نیاز برنامه نویس از آن استفاده کرد. برای مثال می توان نوع نمایش آن را تغییر داد. در قطعه کد زیر، برای نمونه، تغییری در کلاس شمارنده ای که در مثال بالا ارائه کرده بودیم ، می‌دهیم. </p>

```markdown
class Color:
   def __init__(self, name):
       self.name = name

   def __str__(self):
       return self.name

   def __repr__(self):
       return "<Color: %s>" % self

Color.RED = Color("red")
Color.BLUE = Color("blue")

>>> x = Color.RED
>>> x
<Color: red>
>>> x == 1
False
```


You can use the [editor on GitHub](https://github.com/mohammadroghani/research-assignment/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/mohammadroghani/research-assignment/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
