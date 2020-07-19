# Svelte Components

A collection of Svelte components.

## Coverflow

![Coverflow Demo](https://github.com/buhrmi/components/blob/master/gifs/coverflow.gif?raw=true)

[Demo](https://buhrmi.github.io/components/coverflow)

### Usage


```html
<script>
  import { Coverflow } from 'buhrmi'
</script>

<Coverflow {covers}/>
```

#### Props

| Prop | Description | Example |
| --- | --- | --- |
| `covers` | An array containing the url and name of each cover.|`[{url: ..., name: ...}]` |
