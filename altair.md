# Import altair

``` python
import altair as alt
# if in notebook
alt.renderers.enable("notebook")
```

# Histogram

```python
alt.Chart(df).mark_bar().encode(
    x= alt.X('Brain Weight', bin = alt.Bin(maxbins=20) , title= 'Brain Weight Binned'),
    y='count()'
).properties(
    width = 200,
    height=200,
    title='Histogram of Brain Weight'
)
```

# Scatter plot

```python
alt.Chart(df).mark_circle().encode(
    x="Body Weight",
    y="Brain Weight"
)
```

# Line chart

```python
alt.Chart(trends).mark_line().encode(
    x = alt.X("date:T", timeUnit="yearmonth"),
    y = "sum(value)",
    color="search_term"
)
```

# Bar chart

```python
alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="sum(value)",
    color="search_term"
)
```

# Map

# Horizontal concatenation

```python
search_term_barchart|search_term_linechart
```

# Vertical concatenation

```python
search_term_barchart&search_term_linechart
```

# Single selection

```python
select_search_term = alt.selection_single(encodings=["x"])

search_term_linechart = alt.Chart(trends).mark_line().encode(
    x = alt.X("date:T", timeUnit="yearmonth"),
    y = "sum(value)",
    color="search_term"
).transform_filter(
    select_search_term
)

search_term_barchart = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="sum(value)",
    color="search_term"
).properties(
    selection = select_search_term
)

search_term_barchart|search_term_linechart
```

# Interval selection

```python
select_zoom = alt.selection_interval(encodings=["x"])

search_term_linechart = alt.Chart(trends).mark_line().encode(
    x = alt.X("date:T", timeUnit="yearmonth"),
    y = "sum(value)",
    color="search_term",
).transform_filter(
    select_zoom
)

search_term_linechartsmall = alt.Chart(trends).mark_line().encode(
    x = alt.X("date:T", timeUnit="yearmonth"),
    y = "sum(value)",
    color="search_term"
).properties(
    height = 50 ,
    selection = select_zoom
)

search_term_linechart&search_term_linechartsmall
```



















