./kafka-topics.sh --create --topic myTopic --zookeeper <host>:2181 --replication-factor 1 --partitions 2

./kafka-topics.sh --zookeeper <host>:2181 --delete --topic myTopic

./kafka-configs.sh --zookeeper <host>:2181 --entity-type topics --entity-name myTopic --alter --add-config retention.ms=86400000

./kafka-console-consumer.sh --topic myTopic  --bootstrap-server <host>:6667  --property print.key=true --property print.value=true
  
./kafka-consumer-groups.sh --bootstrap-server <host>:9092 --group myGroup --topic myTopic --reset-offsets --to-latest --execute

#consumer LAG 

./kafka-consumer-groups.sh --bootstrap-server <host>:6667 --describe --group myGroup
  
./kafka-consumer-groups.sh --bootstrap-server prdvarkafka01.zb:6667,prdvarkafka02.zb:6667,prdvarkafka03.zb:6667,prdvarkafka04.zb:6667 --group evamIB2 --topic ora_finartprod --reset-offsets --to-datetime '2020-02-26T12:01:28.000' --execute

./kafka-configs.sh --zookeeper <host>:2181 --alter --entity-type topics --add-config retention.ms=1000 --entity-name myTopic 
  
./kafka-configs.sh --zookeeper <host>:2181 --entity-type topics --describe --entity-name myTopic
  
./kafka-configs.sh --zookeeper <host>:2181 --alter --entity-type topics --delete-config retention.ms --entity-name myTopic
  
./kafka-console-consumer.sh --consumer-property group.id=consoleGrup2 --topic myTopic --bootstrap-server host:9092 --from-beginning  

#check topic size

./kafka-consumer-groups.sh  --list --bootstrap-server host:6667 | grep test_consoleGrup1

./kafka-console-consumer.sh --consumer-property group.id=test_consoleGrup1 --topic myTopic --bootstrap-server host:6667

./kafka-consumer-groups.sh --describe --group test_consoleGrup1 --bootstrap-server host:6667

./kafka-consumer-groups.sh --bootstrap-server host:6667 --group test_consoleGrup1 --topic myTopic --reset-offsets --to-datetime '2020-10-01T00:00:00.000' --execute

./kafka-console-consumer.sh --consumer-property group.id=test_consoleGrup1 --topic myTopic --bootstrap-server host:6667 --from-beginning | more

./kafka-consumer-groups.sh --bootstrap-server host:6667 --group test_consoleGrup1 --topic myTopic --reset-offsets --to-earliest --execute

./kafka-log-dirs.sh --describe --bootstrap-server host:9092  --topic-list myTopic | grep -oP '(?<=size":)\d+' | awk '{ sum += $1 } END { print sum }'

#check topic size
