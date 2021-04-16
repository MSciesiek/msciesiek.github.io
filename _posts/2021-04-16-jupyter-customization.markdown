---
layout: post
title:  "Customization of jupyter notebook"
date:   2021-04-16 19:30:59 +0200
categories: jupyter update
---
Changing the default settings of jupyter notebook: I'm using it this often and yet I forget how to do it every time.

{% highlight python %}
import pandas as pd
from IPython.core.display import display, HTML
display(HTML("<style>.container { width:100% !important; }</style>"))
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 1000)
{% endhighlight %}

This maximizes the width of the jupyter cells and increases maximum width of cells in the pandas dataframes.