# GOFAIL-Scenarios-in-Microservices

This was my internship project at NetApp.
It deals with injecting failpoints inside microservices so that they fail to do the work they're supposed to do in some or the other way.
All microservices written in this project are in GO Language.

Fault Injection:
-Method for assessing the reliability on software systems
-For enhancing the testing quality by involving the intentional faults in the software
-Often used in hard-to-simulate failure testing.

Need of a failpoint:
-Errors can happen anywhere, anytime 
-Common Hardware errors related to: Disk, Network, CPU, Clock etc.
-Common Software errors related to: File system, Network protocols etc.
-We need to simulate everything to cover all corner cases.

About GOFAIL:
-An implementation of failpoints for Golang.
-Uses Fail Mechanism.
-Fail Mechanism:  Fault injection at specific places in code.
-Defines failpoints by Comments
gofail enable: converts comments to code
gofail disable: converts code to comments
OFFICIAL DOCUMENTATION OF GOFAIL: https://github.com/etcd-io/gofail

Microservice scenarios for failpoints:
When a service is running, the following cases might arise :
Interrupt
Power failure
System Call
A Higher Priority process comes up
Time Quantum Expired
Some unexpected failure may also occur!!

A SIMPLE SCENARIO: GOFAIL USAGE
func(){
//some code
// gofail: MY DESIRED FAILPOINT HERE
//some more code
}

SCENARIO-1
Returning desired string by triggering failpoint at runtime.
-Standard example given in GOFAIL documentation.
-Intends to give a basic understanding of how GOFAIL works.

SCENARIO-2
-Injecting delay in a microservice that interacts with Mongodb.
-The microservice connects to the MongoDB database and lists all databases present.
Usefulness:
 Sometimes, delay may be noticed while a microservice interacts with a database(MongoDB in our case).
Failure injection checks whether service is able to withstand that delay or not.

SCENARIO-3:
POST API to add a HANA system in hana-system microservice: Add a failpoint while saving data to database.
-Failpoint creates a panic which causes the POST call to fail. However, the GET call works fine. 

SCENARIO-4:
-Blocking a microservice only if it doesn’t retry doing what it is supposed to do.
-Failpoint makes sure that the microservice fails for the first time.
-If the service has the retry logic, it won’t fail from the next time onwards.

SCENARIO-5:
-Simulate a crash of a microservice
-The server doesn’t wait for further requests. It just crashes because of the injected failpoint.
-Such failpoints check whether our microservice is able to withstand such unexpected crashes or not.




