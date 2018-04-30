---
layout: post
title: Usando Jupyter
categories: [Trabajo Corporal]
tags: featured
author: Gustavo G.D.
---


## Estudios con la palabra mindfulness en el título
Aquí una posible imagen:
![png](http://127.0.0.1:4000/fmy_desk/static/minion.png)

### Datos extraidos de PubMed
Para ir a la búqueda ir a [PubMed](https://www.ncbi.nlm.nih.gov/pubmed?term=mindfulness%5BTitle%5D)


```python
#Paquetes:
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

#Los datos:

label = ['1982','1984','1985','1988','1989','1992','1994','1995','1996','1997','1998','1999', '2000', '2001','2002','2003','2004','2005','2006','2007','2008','2009','2010','2011','2012','2013','2014','2015','2016','2017']
studies = [
    1,
    2,
    2,
    1,
    1,
    1,
    2,
    2,
    1,
    3,
    3,
    2,
    5,
    7,
    8,
    15,
    23,
    17,
    27,
    51,
    61,
    90,
    126,
    156,
    187,
    243,
    307,
    418,
    468,
    504
]
print(len(studies), len(label))

```

    30 30



```python
#Plot:
csfont = {'fontname':'Times New Roman'}
def plot_bar_x():
    index = np.arange(len(label))
    plt.bar(index, studies, color='black')
    plt.xlabel('', fontsize=8)
    plt.ylabel('Número de artículos', fontsize=8,)
    plt.xticks(index, label, fontsize=8, rotation=90,)
    #plt.title('Número de artículos con la palabra mindfulness en el título', **csfont)
    plt.savefig('studies_mindfulness.jpg', format='jpg', dpi=500)
    plt.show()
    
y=plot_bar_x()
```


{% include image.html img="output_2_0.jpg" style="wide" lightbox="true" alt="Alt for image" caption="número de artículos con la palabra mindfulness en el título" %}



```python
#Para ver la cantidad de letras disponibles.
import matplotlib.font_manager
matplotlib.font_manager.findSystemFonts(fontpaths=None, fontext='ttf')
```


# Clasificación del número de horas en cada elemento del Experto


```python
import plotly.plotly as py
import plotly.graph_objs as go

values= [140,30,55,100]
labels= ['Teoría y Aplicaciones (140 horas)', 'Práctica Personal (30 horas)', 'Competencias (55 horas)', 'Desarrollo de MBI (100 horas)']
trace = go.Pie(labels=labels, values=values)
py.iplot([trace], filename='basic_pie_chart')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~GustavoDietz/4.embed" height="525px" width="100%"></iframe>



# Comparacion de yoga, mindfulness y meditación:


```python
df_yoga=pd.read_csv('yoga.csv')
#pd.to_numeric(df_yoga['year'], errors='coerce')
#pd.to_numeric(df_yoga['count'], errors='coerce')
pd.to_datetime(df_yoga['year'])
df_yoga.sort_values('count', ascending=True)
df_meditation=pd.read_csv('meditation.csv')
pd.to_datetime(df_meditation['year'])
df_meditation.sort_values('count', ascending=True)
df_mindfulness=pd.read_csv('mindfulness.csv')
pd.to_datetime(df_mindfulness['year'])
df_mindfulness.sort_values('count', ascending=True)
x_yoga=df_yoga['year']
y_yoga=df_yoga['count']
x_meditation=df_meditation['year']
y_meditation=df_meditation['count']
x_mindfulness=df_mindfulness['year']
y_mindfulness=df_mindfulness['count']
```


```python
import plotly.plotly as py
import plotly.graph_objs as go

trace1 = go.Bar(
    x=x_yoga,
    y=y_yoga,
    name='Yoga',
    marker=dict(
        color='rgb(37, 188, 193)'
    )
)
trace2 = go.Bar(
    x=x_meditation,
    y=y_meditation,
    name='Meditation',
    marker=dict(
        color='rgb(237, 150, 25)'
    )
)
trace3 = go.Bar(
    x=x_mindfulness,
    y=y_mindfulness,
    name='Mindfulness',
    marker=dict(
        color='rgb(109, 150, 72)'
    )
)
data = [trace2, trace1, trace3]
layout = go.Layout(
    title='Investigación con palabras Yoga, Meditation y Mindfulness en título',
    xaxis=dict(
        tickfont=dict(
            size=14,
            color='rgb(107, 107, 107)'
        )
    ),
    yaxis=dict(
        title='Número de artículos',
        titlefont=dict(
            size=16,
            color='rgb(107, 107, 107)'
        ),
        tickfont=dict(
            size=14,
            color='rgb(107, 107, 107)'
        )
    ),
    legend=dict(
        x=0,
        y=1.0,
        bgcolor='rgba(255, 255, 255, 0)',
        bordercolor='rgba(255, 255, 255, 0)'
    ),
    barmode='group',
    bargap=0.15,
    bargroupgap=0.1
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='style-bar')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~GustavoDietz/10.embed" height="525px" width="100%"></iframe>




```python
#En una clase de fmy:

values= [1,1,2]
labels= ['Teoría', 'Explicación prácticas', 'Práctica']
trace = go.Pie(labels=labels, values=values)
py.iplot([trace], filename='basic_pie_chart')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~GustavoDietz/4.embed" height="525px" width="100%"></iframe>




```python
#Horas al año del FMY:
values= [120,100,30,104,468]
labels= ['Retiros', 'Clases', 'Reuniones-online', 'Lectura', 'Práctica']
trace = go.Pie(labels=labels, values=values)
py.iplot([trace], filename='basic_pie_chart')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~GustavoDietz/4.embed" height="525px" width="100%"></iframe>




```python
#Suponiendo que duermas 8 horas:
# 6240 horas en 13 meses, de los cuales 822 los dedicas a la meditación, con lo cual: 5418 lo dedicas a otras cosas.
values= [822,5418]
labels= ['Práctica', 'Otras cosas']
trace = go.Pie(labels=labels, values=values)
py.iplot([trace], filename='basic_pie_chart')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~GustavoDietz/4.embed" height="525px" width="100%"></iframe>



