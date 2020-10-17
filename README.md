[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.me/soumilshah1995)



[![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)]


# Elastic Search Query Generator  

#### what is Elastic Search Query Generator ?
* While i was working with Elastic Search i found it very difficult to write complex queries as most of query are deep Nested 
*  Thats the reason i decided to make a helper class that can generate complex Elastic Search query in Seconds 
* Library can be used to generate complex aggregation  Query , Geo location Query (AND | OR | NOT ) any set of combination is possible 
* in addition to all mentioned above you can also generate auto complete query in matter of seconds 
* please see examples below on how to use this module.
* if you have any questions or suggestion please drop me an email at shahsoumil519@gmail.com




## Installation

```bash
pip install elasticsearchquerygenerator
```
## Usage


```python
from elasticsearchquerygenerator.elasticsearchquerygenerator import ElasticSearchQuery

def main():
    helper = ElasticSearchQuery(size=100, BucketName="MyBuckets")

    # match phrase
    query=helper.match_phrase(field="myfeild", value="myvalue", operation='must')

    # terms
    query=helper.terms(field="myfeild", value="myvalue", operation='must')

    # Feild Exists
    query = helper.exists(field='comp feild', operation="must")

    #Match
    query=helper.match(field="MMMMM", value="myvalue", operation='must')

    # Geo Queires
    query = helper.add_geoqueries(radius="100", lat="22", lon="33")

    # Aggreation
    helper.add_aggreation(aggregate_name="FirstName", field="field1",type='terms',sort='desc', size=3)
    helper.add_aggreation(aggregate_name="SecondName", field="field2",type='terms',sort='desc', size=3)
    helper.add_aggreation(aggregate_name="ThirdName", field="field3",type='terms',sort='desc', size=3)
    query = helper.complete_aggreation()
    query = helper.query_string(default_field="DEFAULT",query="X OR  Y",operation='must')

    query = helper.add_geo_aggreation(field="AAAA", lat="22", lon="43",aggregate_name="my_distance")

    print(json.dumps(query, indent=3))


if __name__ == "__main__":
    main()


```
```json
{
   "_source": [],
   "size": 100,
   "min_score": 0.5,
   "query": {
      "bool": {
         "must": [
            {
               "match_phrase": {
                  "myfeild": {
                     "query": "myvalue"
                  }
               }
            },
            {
               "match_phrase": {
                  "myfeild": {
                     "query": "myvalue"
                  }
               }
            },
            {
               "term": {
                  "myfeild": "myvalue"
               }
            },
            {
               "exists": {
                  "field": "comp feild"
               }
            },
            {
               "match": {
                  "MMMMM": {
                     "query": "myvalue"
                  }
               }
            },
            {
               "match": {
                  "MMMMM": {
                     "query": "myvalue"
                  }
               }
            },
            {
               "query_string": {
                  "default_field": "DEFAULT",
                  "query": "X OR  Y"
               }
            }
         ],
         "filter": [
            {
               "geo_distance": {
                  "distance": "100mi",
                  "null": {
                     "lat": "22",
                     "lon": "33"
                  }
               }
            }
         ],
         "should": [],
         "must_not": []
      }
   },
   "aggs": {
      "FirstName": {
         "terms": {
            "field": "field1",
            "order": {
               "_count": "desc"
            },
            "size": 3
         }
      },
      "SecondName": {
         "terms": {
            "field": "field2",
            "order": {
               "_count": "desc"
            },
            "size": 3
         }
      },
      "ThirdName": {
         "terms": {
            "field": "field3",
            "order": {
               "_count": "desc"
            },
            "size": 3
         }
      },
      "my_distance": {
         "geo_distance": {
            "field": "AAAA",
            "origin": "22,43",
            "unit": "mi",
            "ranges": [
               {
                  "to": 0
               },
               {
                  "from": 0,
                  "to": 25
               },
               {
                  "from": 25,
                  "to": 50
               },
               {
                  "from": 50,
                  "to": 75
               },
               {
                  "from": 75,
                  "to": 100
               },
               {
                  "from": 100
               }
            ]
         }
      }
   }
}

```


### Example 2

```python
from elasticsearchquerygenerator.elasticsearchquerygenerator import ElasticSearchQuery

def autocomplete():
    helper = ElasticSearchQuery(size=0, BucketName="MyBuckets")
    query  = helper.autocomplete_1(field="title",value="n", size=25,sort='desc')
    print(json.dumps(query, indent=3))


if __name__ == "__main__":
    main(autocomplete

```

##### i would be adding more examples and making it better and better 

## Authors

## Soumil Nitin Shah 
Bachelor in Electronic Engineering |
Masters in Electrical Engineering | 
Master in Computer Engineering |

* Website : https://soumilshah.herokuapp.com
* Github: https://github.com/soumilshah1995
* Linkedin: https://www.linkedin.com/in/shah-soumil/
* Blog: https://soumilshah1995.blogspot.com/
* Youtube : https://www.youtube.com/channel/UC_eOodxvwS_H7x2uLQa-svw?view_as=subscriber
* Facebook Page : https://www.facebook.com/soumilshah1995/
* Email : shahsoumil519@gmail.com



## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details


