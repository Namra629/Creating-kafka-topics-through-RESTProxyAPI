# Creating-kafka-topics-through-RESTProxyAPI\

1. Get the cluster-id:

       curl -s -X GET 'localhost:8082/v3/clusters'| jq '.data[0].attributes.cluster_id'

2. Get the URL for the topics:

       curl -s -X GET 'localhost:8082/v3/clusters'| jq '.data[0].relationships.topics.links.related'


3.   List the topics:


         curl -s -X GET 'http://localhost:8082/v3/clusters/rgfnzs2RS3O65A7VSpNatg/topics' |jq '.data[].attributes.topic_name'
          "__confluent.support.metrics"
          "_confluent-ksql-confluent_rmoff_01_command_topic"
          "_kafka-connect-01-configs"
          "_kafka-connect-01-offsets"
          "_kafka-connect-01-status"
          "_schemas"
          "confluent_rmoff_01ksql_processing_log"
          "ratings"


4.  Create the topic:

         curl -s -X POST 'http://localhost:8082/v3/clusters/rgfnzs2RS3O65A7VSpNatg/topics' \
         --header 'Content-Type: application/vnd.api+json' \
         --data-raw '{
         "data": {
         "attributes": {
         "topic_name": "rmoff_topic03",
         "partitions_count": 12,
         "replication_factor": 1
         }
         }
         }'


Reference:  https://rmoff.net/2020/06/05/how-to-list-and-create-kafka-topics-using-the-rest-proxy-api/
