
## wordcloud2

[![CRAN](https://www.r-pkg.org/badges/version/wordcloud2)](https://cran.r-project.org/package=wordcloud2)
![Downloads](https://cranlogs.r-pkg.org/badges/wordcloud2)
[![Build status](https://ci.appveyor.com/api/projects/status/wj5afxb1v42h8oui?svg=true)](https://ci.appveyor.com/project/lchiffon/wordcloud2)

R interface to wordcloud for data visualization.
Timdream's [wordcloud2.js](https://github.com/timdream/wordcloud2.js) is used in this package.

## contributors


- [JacobXPX](https://github.com/JacobXPX)
- [AdamSpannbauer](https://github.com/AdamSpannbauer)
- [ekstroem](https://github.com/ekstroem)
- [timelyportfolio](https://github.com/timelyportfolio)
- [AdeelK93](https://github.com/AdeelK93)



### Original description

#### Installation

```
devtools::install_github("lchiffon/wordcloud2")
```
knitr and shiny is support in wordcloud2 package.

#### Example

```
library(wordcloud2)
wordcloud2(demoFreq, size = 1,shape = 'star')
```

![1](examples/img/1.png)


```
wordcloud2(demoFreq, size = 2, minRotation = -pi/2, maxRotation = -pi/2)
```

![1](examples/img/2.png)


```
wordcloud2(demoFreq, size = 2, minRotation = -pi/6, maxRotation = -pi/6,
  rotateRatio = 1)
```

![1](examples/img/3.png)


#### Chinese version
```
## Sys.setlocale("LC_CTYPE","eng")
wordcloud2(demoFreqC, size = 2, fontFamily = "微软雅黑",
           color = "random-light", backgroundColor = "grey")
```

![1](examples/img/4.png)

#### Example of successfully deploying interactivate clickable wordcloud with special shape on R-shiny

Thanks [JacobXPX](https://github.com/JacobXPX)'s contribution to this feature:

Thanks [AdamSpannbauer](https://github.com/AdamSpannbauer) for pointing out the [issues](https://github.com/Lchiffon/wordcloud2/issues/45).

Additional features are added or modified:

1. hover information display are fixed, refering [AdeelK93](https://github.com/AdeelK93)'s previous work, thanks!

2. multiple wordclouds which seperatedly click are supported.

3. `clickedWordInputId` is changed to be automatically generated by: paste0(outputId, "_clicked_word")).

See sample below for more details:

```
library(shiny)
library(wordcloud2)
shinyApp(
  ui=shinyUI(fluidPage(
    #using default clicked word input id
    wordcloud2Output("my_wc", width = "50%", height = "400px"),
    #using custom clicked word input id
    wordcloud2Output("my_wc2", width = "50%", height = "400px"),
    
    verbatimTextOutput("print"),
    verbatimTextOutput("print2")
  )),
  server=shinyServer(function(input,output,session){
    
    figPath = system.file("examples/a.png",package = "wordcloud2")
    
    output$my_wc  = renderWordcloud2(wordcloud2(data = demoFreq, figPath = figPath, size = 0.4,color = "blue"))
    output$my_wc2 = renderWordcloud2(wordcloud2(demoFreq))
    
    #using default clicked word input id
    output$print  = renderPrint(input$my_wc_clicked_word)
    #using custom clicked word input id
    output$print2 = renderPrint(input$my_wc2_clicked_word)
  })
)
```

run the above code and click refresh, it will work.

![1](examples/img/new.gif)