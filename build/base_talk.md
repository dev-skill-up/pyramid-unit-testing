```{=latex}
\usepackage{hyperref}
\usepackage{graphicx}
\usepackage{listings}
\usepackage{textcomp}
\usepackage{fancyvrb}

\newcommand{\passthrough}[1]{\lstset{mathescape=false}#1\lstset{mathescape=true}}
\newcommand{\tightlist}{}
```

```{=latex}
\title{Unit Testing Your Web Application}
\author{Moshe Zadka -- https://cobordism.com}
\date{}

\begin{document}
\begin{titlepage}
\maketitle
\end{titlepage}

\frame{\titlepage}
```

```{=latex}
\begin{frame}
\frametitle{Acknowledgement of Country}

Belmont (in San Francisco Bay Area Peninsula)

Ancestral homeland of the Ramaytush Ohlone people

\end{frame}
```

I live in Belmont,
in the San Francisco Bay Area Peninsula.
I wish to acknowledge it as the
ancestral homeland
of the
Ramaytush Ohlone people.

## Pyramid Example

### Static view

```{=latex}
\begin{frame}[fragile]
\frametitle{Static Value}
```


```python
def empty(request):
    return pyramid.response.Response(
        json.dumps({}).encode("ascii"),
        content_type="application/json",
    )
with pyramid.config.Configurator() as config:
    config.add_route("root", "/")
    config.add_view(empty, route_name="root")
    app = config.make_wsgi_app()
```

```{=latex}
\end{frame}
```

```{=latex}
\begin{frame}[fragile]
\frametitle{Static View Retrieval}
```


```python
request = client.get("/")
request.json()
```




    {}



```{=latex}
\end{frame}
```

### JSON Renderer

```{=latex}
\begin{frame}[fragile]
\frametitle{JSON View}
```


```python
def json(request):
    return {}
with pyramid.config.Configurator() as config:
    config.add_route("root", "/")
    config.add_view(empty, route_name="root")
    config.add_route("json", "/json")
    config.add_view(json, route_name="json", renderer="json")
    app = config.make_wsgi_app()
```

```{=latex}
\end{frame}
```

```{=latex}
\begin{frame}[fragile]
\frametitle{JSON View Retrieval}
```


```python
request = client.get("/json")
request.json()
```




    {}



```{=latex}
\end{frame}
```

### Using Parameters

```{=latex}
\begin{frame}[fragile]
\frametitle{Parameter View}
```


```python
def params(request):
    return dict(thing=request.params["thing"])
with pyramid.config.Configurator() as config:
    config.add_route("root", "/")
    config.add_view(empty, route_name="root")
    config.add_route("json", "/json")
    config.add_view(json, route_name="json", renderer="json")
    config.add_route("params", "/params")
    config.add_view(params, route_name="params", renderer="json")
    app = config.make_wsgi_app()
```

```{=latex}
\end{frame}
```

```{=latex}
\begin{frame}[fragile]
\frametitle{Parameter View Retrieval}
```


```python
request = client.get("/params?thing=hello")
request.json()
```




    {'thing': 'hello'}



```{=latex}
\end{frame}
```

### Using Route Matches

```{=latex}
\begin{frame}[fragile]
\frametitle{Parameter View}
```


```python
def matches(request):
    return dict(name=request.matchdict["name"])
with pyramid.config.Configurator() as config:
    config.add_route("root", "/")
    config.add_view(empty, route_name="root")
    config.add_route("json", "/json")
    config.add_view(json, route_name="json", renderer="json")
    config.add_route("params", "/params")
    config.add_view(params, route_name="params", renderer="json")
    config.add_route("matches", "/matches/{name}")
    config.add_view(matches, route_name="matches", renderer="json")
    app = config.make_wsgi_app()
```

```{=latex}
\end{frame}
```

```{=latex}
\begin{frame}[fragile]
\frametitle{Parameter View Retrieval}
```


```python
request = client.get("/matches/hello")
request.json()
```




    {'name': 'hello'}



```{=latex}
\end{frame}
```

### Using Request Body

```{=latex}
\begin{frame}[fragile]
\frametitle{Body View}
```


```python
def body(request):
    return dict(field=request.json_body["field"])
with pyramid.config.Configurator() as config:
    config.add_route("root", "/")
    config.add_view(empty, route_name="root")
    config.add_route("json", "/json")
    config.add_view(json, route_name="json", renderer="json")
    config.add_route("params", "/params")
    config.add_view(params, route_name="params", renderer="json")
    config.add_route("matches", "/matches/{name}")
    config.add_view(matches, route_name="matches", renderer="json")
    config.add_route("body", "/body")
    config.add_view(body, route_name="body", renderer="json")
    app = config.make_wsgi_app()
```

```{=latex}
\end{frame}
```

```{=latex}
\begin{frame}[fragile]
\frametitle{Body View Retrieval}
```


```python
request = client.post("/body", json=dict(field="hello"))
request.json()
```




    {'field': 'hello'}



```{=latex}
\end{frame}
```

## Pyramid Concepts

### View

### Route

### Configurator

### Registry

### Scanning

## Python Web Concepts

### WSGI

### `httpx`

## Unit Testing

### Mocking Functions

### Mocking Request

### Calling WSGI

### Using `httpx`

## Summary

### Pyramid: Concepts

### Unit Testing: Why?

### Unit Testing: How?

```{=latex}
\end{document}
```
