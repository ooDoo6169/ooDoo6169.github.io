---
layout : post
title: "ggvis_study"
author: "ooDoo"
date: 2018-04-04
categories : ggvis
cover : /assets/article_images/title/instacode_sizedown.png
output: html_document
---



# 1. Dive into plotting with `ggvis`

## 1) basic Usage

{% highlight r %}
layer_points(ggvis(mtcars, x = ~wt, y = ~mpg))
{% endhighlight %}

<!--html_preserve--><div id="plot_id326132734-container" class="ggvis-output-container">
<div id="plot_id326132734" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id326132734_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id326132734" data-renderer="svg">SVG</a>
 | 
<a id="plot_id326132734_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id326132734" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id326132734_download" class="ggvis-download" data-plot-id="plot_id326132734">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id326132734_spec = {
  "data": [
    {
      "name": "mtcars0",
      "format": {
        "type": "csv",
        "parse": {
          "wt": "number",
          "mpg": "number"
        }
      },
      "values": "\"wt\",\"mpg\"\n2.62,21\n2.875,21\n2.32,22.8\n3.215,21.4\n3.44,18.7\n3.46,18.1\n3.57,14.3\n3.19,24.4\n3.15,22.8\n3.44,19.2\n3.44,17.8\n4.07,16.4\n3.73,17.3\n3.78,15.2\n5.25,10.4\n5.424,10.4\n5.345,14.7\n2.2,32.4\n1.615,30.4\n1.835,33.9\n2.465,21.5\n3.52,15.5\n3.435,15.2\n3.84,13.3\n3.845,19.2\n1.935,27.3\n2.14,26\n1.513,30.4\n3.17,15.8\n2.77,19.7\n3.57,15\n2.78,21.4"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n1.31745\n5.61955"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 50
          },
          "x": {
            "scale": "x",
            "field": "data.wt"
          },
          "y": {
            "scale": "y",
            "field": "data.mpg"
          }
        },
        "ggvis": {
          "data": {
            "value": "mtcars0"
          }
        }
      },
      "from": {
        "data": "mtcars0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "wt"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id326132734").parseSpec(plot_id326132734_spec);
</script><!--/html_preserve-->


{% highlight r %}
head(mtcars)
{% endhighlight %}



{% highlight text %}
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
{% endhighlight %}


## 2) Using `dplyr`

{% highlight r %}
library(dplyr)
mtcars %>%
    mutate(disp = disp / 61.0237) %>% # convert engine displacment to litres
    ggvis(x = ~mpg, y = ~disp) %>%
    layer_points() 
{% endhighlight %}

<!--html_preserve--><div id="plot_id914767627-container" class="ggvis-output-container">
<div id="plot_id914767627" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id914767627_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id914767627" data-renderer="svg">SVG</a>
 | 
<a id="plot_id914767627_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id914767627" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id914767627_download" class="ggvis-download" data-plot-id="plot_id914767627">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id914767627_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"mpg\",\"disp\"\n21,2.62193213456411\n21,2.62193213456411\n22.8,1.76980419083078\n21.4,4.22786556698463\n18.7,5.89934730276925\n18.1,3.68709206423078\n14.3,5.89934730276925\n24.4,2.40398402587847\n22.8,2.30730027841642\n19.2,2.74647391095591\n17.8,2.74647391095591\n16.4,4.51955551695489\n17.3,4.51955551695489\n15.2,4.51955551695489\n10.4,7.73469979696413\n10.4,7.53805488687182\n14.7,7.21031337005131\n32.4,1.28966286868872\n30.4,1.24050164116565\n33.9,1.16512109229693\n21.5,1.96808780850719\n15.5,5.21109011744617\n15.2,4.98167105567181\n13.3,5.735476544359\n19.2,6.55483033641028\n27.3,1.29457899144103\n26,1.97136522367539\n30.4,1.55841091248154\n15.8,5.75186362020002\n19.7,2.37612599694873\n15,4.93250982814874\n21.4,1.98283617676411"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n0.836642157063567\n8.06317873219749"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 50
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id914767627").parseSpec(plot_id914767627_spec);
</script><!--/html_preserve-->
*변수 앞에 "~"를 붙이는 이유*
 : ggvis안에서 사용하려는 변수는 실제 벡터 혙태로 저장 되어있는 변수가 아닌, 해당 데이터셋에서만 존재하는 컬럼이기에 이를 구분해 주기 위해서 반드시 "~"를 앞에 붙여야 한다. 
 
## 3) Mapping tools
 - `fill`
 - `stroke` 
 - `size`
 - `shape`
 
### (1) fill 

{% highlight r %}
# factors
mtcars %>% 
    ggvis(~mpg, ~disp, fill = ~as.factor(vs)) %>% 
    layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id521201551-container" class="ggvis-output-container">
<div id="plot_id521201551" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id521201551_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id521201551" data-renderer="svg">SVG</a>
 | 
<a id="plot_id521201551_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id521201551" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id521201551_download" class="ggvis-download" data-plot-id="plot_id521201551">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id521201551_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"as.factor(vs)\",\"mpg\",\"disp\"\n\"0\",21,160\n\"0\",21,160\n\"1\",22.8,108\n\"1\",21.4,258\n\"0\",18.7,360\n\"1\",18.1,225\n\"0\",14.3,360\n\"1\",24.4,146.7\n\"1\",22.8,140.8\n\"1\",19.2,167.6\n\"1\",17.8,167.6\n\"0\",16.4,275.8\n\"0\",17.3,275.8\n\"0\",15.2,275.8\n\"0\",10.4,472\n\"0\",10.4,460\n\"0\",14.7,440\n\"1\",32.4,78.7\n\"1\",30.4,75.7\n\"1\",33.9,71.1\n\"1\",21.5,120.1\n\"0\",15.5,318\n\"0\",15.2,304\n\"0\",13.3,350\n\"0\",19.2,400\n\"1\",27.3,79\n\"0\",26,120.3\n\"1\",30.4,95.1\n\"0\",15.8,351\n\"0\",19.7,145\n\"0\",15,301\n\"1\",21.4,121"
    },
    {
      "name": "scale/fill",
      "format": {
        "type": "csv",
        "parse": {}
      },
      "values": "\"domain\"\n\"0\"\n\"1\""
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "fill",
      "type": "ordinal",
      "domain": {
        "data": "scale/fill",
        "field": "data.domain"
      },
      "points": true,
      "sort": false,
      "range": "category10"
    },
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "size": {
            "value": 50
          },
          "fill": {
            "scale": "fill",
            "field": "data.as\\.factor(vs)"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [
    {
      "orient": "right",
      "fill": "fill",
      "title": "as.factor(vs)"
    }
  ],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id521201551").parseSpec(plot_id521201551_spec);
</script><!--/html_preserve-->

{% highlight r %}
# numeric
mtcars %>% 
    ggvis(~mpg, ~disp, fill = ~qsec) %>% 
    layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id832915705-container" class="ggvis-output-container">
<div id="plot_id832915705" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id832915705_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id832915705" data-renderer="svg">SVG</a>
 | 
<a id="plot_id832915705_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id832915705" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id832915705_download" class="ggvis-download" data-plot-id="plot_id832915705">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id832915705_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "qsec": "number",
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"qsec\",\"mpg\",\"disp\"\n16.46,21,160\n17.02,21,160\n18.61,22.8,108\n19.44,21.4,258\n17.02,18.7,360\n20.22,18.1,225\n15.84,14.3,360\n20,24.4,146.7\n22.9,22.8,140.8\n18.3,19.2,167.6\n18.9,17.8,167.6\n17.4,16.4,275.8\n17.6,17.3,275.8\n18,15.2,275.8\n17.98,10.4,472\n17.82,10.4,460\n17.42,14.7,440\n19.47,32.4,78.7\n18.52,30.4,75.7\n19.9,33.9,71.1\n20.01,21.5,120.1\n16.87,15.5,318\n17.3,15.2,304\n15.41,13.3,350\n17.05,19.2,400\n18.9,27.3,79\n16.7,26,120.3\n16.9,30.4,95.1\n14.5,15.8,351\n15.5,19.7,145\n14.6,15,301\n18.6,21.4,121"
    },
    {
      "name": "scale/fill",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n14.5\n22.9"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "fill",
      "domain": {
        "data": "scale/fill",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": ["#132B43", "#56B1F7"]
    },
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "size": {
            "value": 50
          },
          "fill": {
            "scale": "fill",
            "field": "data.qsec"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [
    {
      "orient": "right",
      "fill": "fill",
      "title": "qsec"
    }
  ],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id832915705").parseSpec(plot_id832915705_spec);
</script><!--/html_preserve-->

{% highlight r %}
# fixed colour
mtcars %>% 
    ggvis(~mpg, ~disp, fill := "skyblue") %>% 
    layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id736129884-container" class="ggvis-output-container">
<div id="plot_id736129884" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id736129884_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id736129884" data-renderer="svg">SVG</a>
 | 
<a id="plot_id736129884_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id736129884" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id736129884_download" class="ggvis-download" data-plot-id="plot_id736129884">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id736129884_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"mpg\",\"disp\"\n21,160\n21,160\n22.8,108\n21.4,258\n18.7,360\n18.1,225\n14.3,360\n24.4,146.7\n22.8,140.8\n19.2,167.6\n17.8,167.6\n16.4,275.8\n17.3,275.8\n15.2,275.8\n10.4,472\n10.4,460\n14.7,440\n32.4,78.7\n30.4,75.7\n33.9,71.1\n21.5,120.1\n15.5,318\n15.2,304\n13.3,350\n19.2,400\n27.3,79\n26,120.3\n30.4,95.1\n15.8,351\n19.7,145\n15,301\n21.4,121"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "size": {
            "value": 50
          },
          "fill": {
            "value": "skyblue"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id736129884").parseSpec(plot_id736129884_spec);
</script><!--/html_preserve-->
: same as ggplot's usage, but If you want to make the points a fixed colour or size, you need to use `:=` instead of `=`. 
 
### (2) stroke 

{% highlight r %}
# setting the stroke color using varialbe
mtcars %>%
    ggvis(~mpg, ~disp, stroke = ~vs) %>%
    layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id476106844-container" class="ggvis-output-container">
<div id="plot_id476106844" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id476106844_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id476106844" data-renderer="svg">SVG</a>
 | 
<a id="plot_id476106844_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id476106844" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id476106844_download" class="ggvis-download" data-plot-id="plot_id476106844">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id476106844_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "vs": "number",
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"vs\",\"mpg\",\"disp\"\n0,21,160\n0,21,160\n1,22.8,108\n1,21.4,258\n0,18.7,360\n1,18.1,225\n0,14.3,360\n1,24.4,146.7\n1,22.8,140.8\n1,19.2,167.6\n1,17.8,167.6\n0,16.4,275.8\n0,17.3,275.8\n0,15.2,275.8\n0,10.4,472\n0,10.4,460\n0,14.7,440\n1,32.4,78.7\n1,30.4,75.7\n1,33.9,71.1\n1,21.5,120.1\n0,15.5,318\n0,15.2,304\n0,13.3,350\n0,19.2,400\n1,27.3,79\n0,26,120.3\n1,30.4,95.1\n0,15.8,351\n0,19.7,145\n0,15,301\n1,21.4,121"
    },
    {
      "name": "scale/stroke",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n0\n1"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "stroke",
      "domain": {
        "data": "scale/stroke",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": ["#132B43", "#56B1F7"]
    },
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 50
          },
          "stroke": {
            "scale": "stroke",
            "field": "data.vs"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [
    {
      "orient": "right",
      "stroke": "stroke",
      "title": "vs"
    }
  ],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id476106844").parseSpec(plot_id476106844_spec);
</script><!--/html_preserve-->

{% highlight r %}
# setting the stroke color using the fixed colour 
mtcars %>%
    ggvis(~mpg, ~disp, stroke := "black") %>%
    layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id237864035-container" class="ggvis-output-container">
<div id="plot_id237864035" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id237864035_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id237864035" data-renderer="svg">SVG</a>
 | 
<a id="plot_id237864035_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id237864035" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id237864035_download" class="ggvis-download" data-plot-id="plot_id237864035">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id237864035_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"mpg\",\"disp\"\n21,160\n21,160\n22.8,108\n21.4,258\n18.7,360\n18.1,225\n14.3,360\n24.4,146.7\n22.8,140.8\n19.2,167.6\n17.8,167.6\n16.4,275.8\n17.3,275.8\n15.2,275.8\n10.4,472\n10.4,460\n14.7,440\n32.4,78.7\n30.4,75.7\n33.9,71.1\n21.5,120.1\n15.5,318\n15.2,304\n13.3,350\n19.2,400\n27.3,79\n26,120.3\n30.4,95.1\n15.8,351\n19.7,145\n15,301\n21.4,121"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 50
          },
          "stroke": {
            "value": "black"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id237864035").parseSpec(plot_id237864035_spec);
</script><!--/html_preserve-->
 
### (3) size

{% highlight r %}
mtcars %>%
    ggvis(~mpg, ~disp, size = ~vs) %>% 
    layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id468156349-container" class="ggvis-output-container">
<div id="plot_id468156349" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id468156349_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id468156349" data-renderer="svg">SVG</a>
 | 
<a id="plot_id468156349_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id468156349" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id468156349_download" class="ggvis-download" data-plot-id="plot_id468156349">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id468156349_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "vs": "number",
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"vs\",\"mpg\",\"disp\"\n0,21,160\n0,21,160\n1,22.8,108\n1,21.4,258\n0,18.7,360\n1,18.1,225\n0,14.3,360\n1,24.4,146.7\n1,22.8,140.8\n1,19.2,167.6\n1,17.8,167.6\n0,16.4,275.8\n0,17.3,275.8\n0,15.2,275.8\n0,10.4,472\n0,10.4,460\n0,14.7,440\n1,32.4,78.7\n1,30.4,75.7\n1,33.9,71.1\n1,21.5,120.1\n0,15.5,318\n0,15.2,304\n0,13.3,350\n0,19.2,400\n1,27.3,79\n0,26,120.3\n1,30.4,95.1\n0,15.8,351\n0,19.7,145\n0,15,301\n1,21.4,121"
    },
    {
      "name": "scale/size",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n0\n1"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "size",
      "domain": {
        "data": "scale/size",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": [20, 100]
    },
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "scale": "size",
            "field": "data.vs"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [
    {
      "orient": "right",
      "size": "size",
      "title": "vs"
    }
  ],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id468156349").parseSpec(plot_id468156349_spec);
</script><!--/html_preserve-->
 

### (4) shape

{% highlight r %}
# shape  
mtcars %>% 
    ggvis(~mpg, ~disp, shape := "diamond") %>%
    layer_points() 
{% endhighlight %}

<!--html_preserve--><div id="plot_id229175646-container" class="ggvis-output-container">
<div id="plot_id229175646" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id229175646_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id229175646" data-renderer="svg">SVG</a>
 | 
<a id="plot_id229175646_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id229175646" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id229175646_download" class="ggvis-download" data-plot-id="plot_id229175646">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id229175646_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"mpg\",\"disp\"\n21,160\n21,160\n22.8,108\n21.4,258\n18.7,360\n18.1,225\n14.3,360\n24.4,146.7\n22.8,140.8\n19.2,167.6\n17.8,167.6\n16.4,275.8\n17.3,275.8\n15.2,275.8\n10.4,472\n10.4,460\n14.7,440\n32.4,78.7\n30.4,75.7\n33.9,71.1\n21.5,120.1\n15.5,318\n15.2,304\n13.3,350\n19.2,400\n27.3,79\n26,120.3\n30.4,95.1\n15.8,351\n19.7,145\n15,301\n21.4,121"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 50
          },
          "shape": {
            "value": "diamond"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id229175646").parseSpec(plot_id229175646_spec);
</script><!--/html_preserve-->

{% highlight r %}
# shape differently as variable
mtcars %>% 
    ggvis(~mpg, ~disp, shape = ~factor(cyl)) %>%
    layer_points() 
{% endhighlight %}

<!--html_preserve--><div id="plot_id699812399-container" class="ggvis-output-container">
<div id="plot_id699812399" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id699812399_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id699812399" data-renderer="svg">SVG</a>
 | 
<a id="plot_id699812399_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id699812399" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id699812399_download" class="ggvis-download" data-plot-id="plot_id699812399">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id699812399_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"factor(cyl)\",\"mpg\",\"disp\"\n\"6\",21,160\n\"6\",21,160\n\"4\",22.8,108\n\"6\",21.4,258\n\"8\",18.7,360\n\"6\",18.1,225\n\"8\",14.3,360\n\"4\",24.4,146.7\n\"4\",22.8,140.8\n\"6\",19.2,167.6\n\"6\",17.8,167.6\n\"8\",16.4,275.8\n\"8\",17.3,275.8\n\"8\",15.2,275.8\n\"8\",10.4,472\n\"8\",10.4,460\n\"8\",14.7,440\n\"4\",32.4,78.7\n\"4\",30.4,75.7\n\"4\",33.9,71.1\n\"4\",21.5,120.1\n\"8\",15.5,318\n\"8\",15.2,304\n\"8\",13.3,350\n\"8\",19.2,400\n\"4\",27.3,79\n\"4\",26,120.3\n\"4\",30.4,95.1\n\"8\",15.8,351\n\"6\",19.7,145\n\"8\",15,301\n\"4\",21.4,121"
    },
    {
      "name": "scale/shape",
      "format": {
        "type": "csv",
        "parse": {}
      },
      "values": "\"domain\"\n\"4\"\n\"6\"\n\"8\""
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "shape",
      "type": "ordinal",
      "domain": {
        "data": "scale/shape",
        "field": "data.domain"
      },
      "points": true,
      "sort": false,
      "range": "shapes"
    },
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 50
          },
          "shape": {
            "scale": "shape",
            "field": "data.factor(cyl)"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [
    {
      "orient": "right",
      "shape": "shape",
      "title": "factor(cyl)"
    }
  ],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id699812399").parseSpec(plot_id699812399_spec);
</script><!--/html_preserve-->

{% highlight r %}
# shape and color
mtcars %>% 
    ggvis(~mpg, ~disp, shape = ~factor(cyl), fill = ~as.factor(cyl)) %>%
    layer_points() 
{% endhighlight %}

<!--html_preserve--><div id="plot_id157691303-container" class="ggvis-output-container">
<div id="plot_id157691303" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id157691303_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id157691303" data-renderer="svg">SVG</a>
 | 
<a id="plot_id157691303_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id157691303" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id157691303_download" class="ggvis-download" data-plot-id="plot_id157691303">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id157691303_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "mpg": "number",
          "disp": "number"
        }
      },
      "values": "\"factor(cyl)\",\"as.factor(cyl)\",\"mpg\",\"disp\"\n\"6\",\"6\",21,160\n\"6\",\"6\",21,160\n\"4\",\"4\",22.8,108\n\"6\",\"6\",21.4,258\n\"8\",\"8\",18.7,360\n\"6\",\"6\",18.1,225\n\"8\",\"8\",14.3,360\n\"4\",\"4\",24.4,146.7\n\"4\",\"4\",22.8,140.8\n\"6\",\"6\",19.2,167.6\n\"6\",\"6\",17.8,167.6\n\"8\",\"8\",16.4,275.8\n\"8\",\"8\",17.3,275.8\n\"8\",\"8\",15.2,275.8\n\"8\",\"8\",10.4,472\n\"8\",\"8\",10.4,460\n\"8\",\"8\",14.7,440\n\"4\",\"4\",32.4,78.7\n\"4\",\"4\",30.4,75.7\n\"4\",\"4\",33.9,71.1\n\"4\",\"4\",21.5,120.1\n\"8\",\"8\",15.5,318\n\"8\",\"8\",15.2,304\n\"8\",\"8\",13.3,350\n\"8\",\"8\",19.2,400\n\"4\",\"4\",27.3,79\n\"4\",\"4\",26,120.3\n\"4\",\"4\",30.4,95.1\n\"8\",\"8\",15.8,351\n\"6\",\"6\",19.7,145\n\"8\",\"8\",15,301\n\"4\",\"4\",21.4,121"
    },
    {
      "name": "scale/fill",
      "format": {
        "type": "csv",
        "parse": {}
      },
      "values": "\"domain\"\n\"4\"\n\"6\"\n\"8\""
    },
    {
      "name": "scale/shape",
      "format": {
        "type": "csv",
        "parse": {}
      },
      "values": "\"domain\"\n\"4\"\n\"6\"\n\"8\""
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n51.055\n492.045"
    }
  ],
  "scales": [
    {
      "name": "fill",
      "type": "ordinal",
      "domain": {
        "data": "scale/fill",
        "field": "data.domain"
      },
      "points": true,
      "sort": false,
      "range": "category10"
    },
    {
      "name": "shape",
      "type": "ordinal",
      "domain": {
        "data": "scale/shape",
        "field": "data.domain"
      },
      "points": true,
      "sort": false,
      "range": "shapes"
    },
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "size": {
            "value": 50
          },
          "shape": {
            "scale": "shape",
            "field": "data.factor(cyl)"
          },
          "fill": {
            "scale": "fill",
            "field": "data.as\\.factor(cyl)"
          },
          "x": {
            "scale": "x",
            "field": "data.mpg"
          },
          "y": {
            "scale": "y",
            "field": "data.disp"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [
    {
      "orient": "right",
      "fill": "fill",
      "title": "as.factor(cyl)"
    },
    {
      "orient": "right",
      "shape": "shape",
      "title": "factor(cyl)"
    }
  ],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "disp"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id157691303").parseSpec(plot_id157691303_spec);
</script><!--/html_preserve-->
*i don't know how to readjust the legend in ggvis yet*

 
### (5) opacity(alpha value in ggplot)

{% highlight r %}
mtcars %>% 
    ggvis(~wt, ~mpg, size := 300, opacity := 0.4) %>%
    layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id334797291-container" class="ggvis-output-container">
<div id="plot_id334797291" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id334797291_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id334797291" data-renderer="svg">SVG</a>
 | 
<a id="plot_id334797291_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id334797291" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id334797291_download" class="ggvis-download" data-plot-id="plot_id334797291">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id334797291_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "wt": "number",
          "mpg": "number"
        }
      },
      "values": "\"wt\",\"mpg\"\n2.62,21\n2.875,21\n2.32,22.8\n3.215,21.4\n3.44,18.7\n3.46,18.1\n3.57,14.3\n3.19,24.4\n3.15,22.8\n3.44,19.2\n3.44,17.8\n4.07,16.4\n3.73,17.3\n3.78,15.2\n5.25,10.4\n5.424,10.4\n5.345,14.7\n2.2,32.4\n1.615,30.4\n1.835,33.9\n2.465,21.5\n3.52,15.5\n3.435,15.2\n3.84,13.3\n3.845,19.2\n1.935,27.3\n2.14,26\n1.513,30.4\n3.17,15.8\n2.77,19.7\n3.57,15\n2.78,21.4"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n1.31745\n5.61955"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 300
          },
          "opacity": {
            "value": 0.4
          },
          "x": {
            "scale": "x",
            "field": "data.wt"
          },
          "y": {
            "scale": "y",
            "field": "data.mpg"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "wt"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id334797291").parseSpec(plot_id334797291_spec);
</script><!--/html_preserve-->
 
 
#2. Interaction_using mouse
## (1) input_slider() 
### (1) control the size and opacity 

{% highlight r %}
mtcars %>% 
  ggvis(~wt, ~mpg, 
    size := input_slider(10, 100),
    opacity := input_slider(0, 1)) %>% 
  layer_points()
{% endhighlight %}

<!--html_preserve--><div id="plot_id343987709-container" class="ggvis-output-container">
<div id="plot_id343987709" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id343987709_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id343987709" data-renderer="svg">SVG</a>
 | 
<a id="plot_id343987709_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id343987709" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id343987709_download" class="ggvis-download" data-plot-id="plot_id343987709">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id343987709_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "reactive_960412100": "number",
          "reactive_369371707": "number",
          "wt": "number",
          "mpg": "number"
        }
      },
      "values": "\"reactive_960412100\",\"reactive_369371707\",\"wt\",\"mpg\"\n55,0.5,2.62,21\n55,0.5,2.875,21\n55,0.5,2.32,22.8\n55,0.5,3.215,21.4\n55,0.5,3.44,18.7\n55,0.5,3.46,18.1\n55,0.5,3.57,14.3\n55,0.5,3.19,24.4\n55,0.5,3.15,22.8\n55,0.5,3.44,19.2\n55,0.5,3.44,17.8\n55,0.5,4.07,16.4\n55,0.5,3.73,17.3\n55,0.5,3.78,15.2\n55,0.5,5.25,10.4\n55,0.5,5.424,10.4\n55,0.5,5.345,14.7\n55,0.5,2.2,32.4\n55,0.5,1.615,30.4\n55,0.5,1.835,33.9\n55,0.5,2.465,21.5\n55,0.5,3.52,15.5\n55,0.5,3.435,15.2\n55,0.5,3.84,13.3\n55,0.5,3.845,19.2\n55,0.5,1.935,27.3\n55,0.5,2.14,26\n55,0.5,1.513,30.4\n55,0.5,3.17,15.8\n55,0.5,2.77,19.7\n55,0.5,3.57,15\n55,0.5,2.78,21.4"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n1.31745\n5.61955"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "field": "data.reactive_960412100"
          },
          "opacity": {
            "field": "data.reactive_369371707"
          },
          "x": {
            "scale": "x",
            "field": "data.wt"
          },
          "y": {
            "scale": "y",
            "field": "data.mpg"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "wt"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id343987709").parseSpec(plot_id343987709_spec);
</script><!--/html_preserve-->

*the result gonna show on the *Viewer of Rstudio
if we want pass the next step, we have to quit the result such as shiny-apps

### (2) width and centers of histogram bins

{% highlight r %}
mtcars %>% 
    ggvis(~wt) %>% # since histogram only takes list of data type, indexing the value as above using "~""
    layer_histograms(width = input_slider(0, 4, step = 0.10, label = "width"),
                     center = input_slider(0, 2, step = 0.05, label = "center"))
{% endhighlight %}

<!--html_preserve--><div id="plot_id122745455-container" class="ggvis-output-container">
<div id="plot_id122745455" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id122745455_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id122745455" data-renderer="svg">SVG</a>
 | 
<a id="plot_id122745455_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id122745455" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id122745455_download" class="ggvis-download" data-plot-id="plot_id122745455">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id122745455_spec = {
  "data": [
    {
      "name": ".0/bin1/stack2",
      "format": {
        "type": "csv",
        "parse": {
          "xmin_": "number",
          "xmax_": "number",
          "stack_upr_": "number",
          "stack_lwr_": "number"
        }
      },
      "values": "\"xmin_\",\"xmax_\",\"stack_upr_\",\"stack_lwr_\"\n0,2,4,0\n2,4,24,0\n4,6,4,0"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n-0.3\n6.3"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n0\n25.2"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "rect",
      "properties": {
        "update": {
          "stroke": {
            "value": "#000000"
          },
          "fill": {
            "value": "#333333"
          },
          "x": {
            "scale": "x",
            "field": "data.xmin_"
          },
          "x2": {
            "scale": "x",
            "field": "data.xmax_"
          },
          "y": {
            "scale": "y",
            "field": "data.stack_upr_"
          },
          "y2": {
            "scale": "y",
            "field": "data.stack_lwr_"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0/bin1/stack2"
          }
        }
      },
      "from": {
        "data": ".0/bin1/stack2"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "wt"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "count"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id122745455").parseSpec(plot_id122745455_spec);
</script><!--/html_preserve-->


## (2) input_checkbox





#2. Interaction_using keyboard

{% highlight r %}
keys_s <- left_right(10, 1000, step = 50)
mtcars %>%
    ggvis(~wt, ~mpg, size := keys_s, opacity := 0.5) %>% 
    layer_points() 
{% endhighlight %}

<!--html_preserve--><div id="plot_id327404088-container" class="ggvis-output-container">
<div id="plot_id327404088" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id327404088_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id327404088" data-renderer="svg">SVG</a>
 | 
<a id="plot_id327404088_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id327404088" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id327404088_download" class="ggvis-download" data-plot-id="plot_id327404088">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id327404088_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "reactive_850350233": "number",
          "wt": "number",
          "mpg": "number"
        }
      },
      "values": "\"reactive_850350233\",\"wt\",\"mpg\"\n505,2.62,21\n505,2.875,21\n505,2.32,22.8\n505,3.215,21.4\n505,3.44,18.7\n505,3.46,18.1\n505,3.57,14.3\n505,3.19,24.4\n505,3.15,22.8\n505,3.44,19.2\n505,3.44,17.8\n505,4.07,16.4\n505,3.73,17.3\n505,3.78,15.2\n505,5.25,10.4\n505,5.424,10.4\n505,5.345,14.7\n505,2.2,32.4\n505,1.615,30.4\n505,1.835,33.9\n505,2.465,21.5\n505,3.52,15.5\n505,3.435,15.2\n505,3.84,13.3\n505,3.845,19.2\n505,1.935,27.3\n505,2.14,26\n505,1.513,30.4\n505,3.17,15.8\n505,2.77,19.7\n505,3.57,15\n505,2.78,21.4"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n1.31745\n5.61955"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n9.225\n35.075"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "field": "data.reactive_850350233"
          },
          "opacity": {
            "value": 0.5
          },
          "x": {
            "scale": "x",
            "field": "data.wt"
          },
          "y": {
            "scale": "y",
            "field": "data.mpg"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "wt"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "mpg"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 1440,
    "height": 1008
  },
  "handlers": null
};
ggvis.getPlot("plot_id327404088").parseSpec(plot_id327404088_spec);
</script><!--/html_preserve-->



{% highlight r %}
#knit2html(input = "C:/Users/TaeHwan/Desktop/0. R/12. ggvis/ggvis_study.Rmd", output = "C:/Users/TaeHwan/Desktop/0. R/12. ggvis") 
{% endhighlight %}









