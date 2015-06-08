# emprouter
Simple Edge Messaging Protocol (EMP) message router supporting AMQP and ClassD


Introduction:
-----------------------------------
The EMPRouter is a test tool written in Java that allows ITC clients to send EMP messages via either ClassD or AMQP.
The EMPRouter receives the messages and routes them to other clients according to the destination EMP address in the
messages.  A simple EMP client is also included allowing the sending and receiving of test messages via either ClassD
or AMQP.


Build Instructions:
------------------------------------
To build, first install JDK 1.6 or later and Apache Ant 1.6 or later. To build the code type:

"ant build"

(note: pom.xml does not work yet, neet to upgrade QPID to version 0.32)


Configuration:
-------------------------------------
Configuration is provided in the file "config/emprouter.cfg"
EMP ClassD and AMQP endpoints can be added by inserting lines into this comma delimited file.  The sytax is as follows:

"EMP_ADDRESS,TYPE,QUEUE_NAME or PORT"

TYPE should be set to AMQP or CLASSD.  

For AMQP, a QUEUE_NAME is required.  This will be the name of the queue from which the corresponding AMQP application
will receive incoming messages.  AMPQ applications should always send message to the exchange "FromApp.Ex" using routing key "FromAppQueueToApp.Ex".

For CLASSD, a PORT value is required.  This is the port to and from which the ClassD application will send and receive
messages.

Running:
-------------------------------------

To start the EMPRouter, execute the script "emprouter.sh"


Testing:
-------------------------------------

To test the EMProuter, use the script "empclient.sh".  This script sends a "Hello, EMP" message to the emprouter and
will also listen for inbound messages and display any that are recieved.  For instance, you can start two EMP clients,
 one AMQP and one CLASSD.  For AMQP, type:

"./empclient.sh RRAA.b:am rraa_b_am"

Note, the queue name "rraa_b_am" must match a valid queue name from the emprouter.cfg config file.

For CLASSD, type:

"./empclient.sh RRAA.b:sma01 4441"


Both client instances will prompt you for the EMP address to which a hello world message can be sent.  From the AMQP
client, type:

"RRAA.b:sma01"

and from the CLASSD client, type:

"RRAA.b:am"


You should see the "Hello, EMP" messages recieved at the correct destinations.

 




