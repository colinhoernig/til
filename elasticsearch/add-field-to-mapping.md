# Adding Fields To ElasticSearch Index Mapping
_02/24/2016_

ElasticSearch is a very powerful tool for indexing, searching, and analyzing data.
Setting up field mappings can be quite tricky.  Adding a field to an ES mapping is
actually quite simple.

```bash
$ curl -X POST 'http://localhost:9200/yourindexname/_mapping/yourindextype' -d \'
{
  "properties": {
    "your_field_name": {
      "type": "string",
      "fields": {
        "analyzed": {
          "type": "string"
        },
        "str": {
          "type": "string",
          "index": "not_analyzed"
        }
      }
    },
    // ... other fields here
  }
}
'
```

More info on PUT mappings can be found [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-put-mapping.html)
