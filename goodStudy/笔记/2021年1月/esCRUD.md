    PUT /test1/type1/1
    {
      "name":"狂神说",
      "age":13
    }
```bash
PUT /test2
{
  "mappings":{
    "properties":{
      "name":{
        "type": "text"
      },
      "age":{
        "type":"long"
      },
      "birthday":{
        "type":"date"
      }
      
    }
  }
}
```

```bash
PUT /test4/_doc/2
{
  "name":"狂神说",
  "age":13,
  "birth":"1997-01-05"
}

GET _cat/health

GET _cat/indices?v
```

![](https://pic.downk.cc/item/5fbfd54d15e77190842bd6d6.png)
![](https://pic.downk.cc/item/5fbfd54d15e77190842bd6d8.png)
![](https://pic.downk.cc/item/5fbfd54d15e77190842bd6da.png)
![](https://pic.downk.cc/item/5fbfd54d15e77190842bd6dc.png)
![](https://pic.downk.cc/item/5fbfd53c15e77190842bd287.png)