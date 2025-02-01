# tinysearch

full-text search in <500 lines of code

```javascript
const TinySearch = require('tinysearch')

const index = new TinySearch()

// add documents
index.add({ id: 1, text: 'hello world' })
index.add({ id: 2, text: 'world of search' })

// search
const results = index.search('world')
// [{ id: 1, score: 0.8 }, { id: 2, score: 0.9 }]
```

## features

- stemming
- stop words
- tf-idf ranking
- fuzzy matching
- phrase search

## no dependencies

pure javascript. works in browser and node.

## size

- minified: 8kb
- gzipped: 3kb

## api

```javascript
// add with fields
index.add({
  id: 1,
  title: 'Getting Started',
  body: 'This is a guide...',
  tags: ['tutorial', 'beginner']
})

// search specific field
index.search('guide', { field: 'body' })

// fuzzy search (typo tolerance)
index.search('tutrial', { fuzzy: true })

// phrase search
index.search('"getting started"')

// boost fields
index.search('guide', {
  boost: { title: 2, body: 1 }
})
```

## persistence

```javascript
// export index
const data = index.export()
localStorage.setItem('search-index', data)

// import index
const data = localStorage.getItem('search-index')
const index = TinySearch.import(data)
```

## performance

| docs | index time | search time |
|------|------------|-------------|
| 100 | 12ms | <1ms |
| 1k | 89ms | 2ms |
| 10k | 743ms | 8ms |

## alternatives

- lunr.js (30kb, more features)
- elasticlunr (25kb, faster)
- fuse.js (fuzzy only)

MIT • [npm](https://www.npmjs.com/package/tinysearch)
