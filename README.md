## kubernetes-adminssion-controll-with-OPA

RBAG has been proved not enough in todays problem domains. We have so many scenarios where policy based authorization is wildly necessery. Project OPA (Open poilicy Agent) can be a good option that can take care of your policies in a standard way. OPA is a general purpose policy engine, this is why we  may levarage OPA in use cases other than access controll. It can work as a full fledged rule engine too.

## How OPA can be integrated?

- We can deploy OPA service as a separate microservice where it will work as a decision maker or evaluator. Other microservices will call OPA- service api to get the decision.
- If our microservice is written in go, OPA can be integrated as a pakgage.


OPA uses rego- a declarative language for authoring policies, takes json as input and holds facts or data as json . Using OPA, we can make decision like,

- Should this API call be allowed? ``` E.g., true or false.```
- How much quota remains for this user? ``` E.g., 1048.```
- Which hosts can this container be deployed on? ``` E.g., ["host1", "host40", ..., "host329"].```
- What updates must be applied to this resource? ``` E.g., {"labels": {"team": "products}}.```


How OPA Makes decsion,

As we discussed earclier, OPA usages three resource to make a decision,

### Data: Data is the fact on which OPA's evaluator will make decision. Data must be in ``` json ``` format.
  
Example, 
```
{
  "shahidul": [
    "read",
    "write"
  ],
  "Apon": [
    "read"
  ]
}
```
By the data example above, we're provably saying, shahidul can read and write a certain resource and Apon can only read that reaource.

### Input: Input is actually a question which must be presented in ``` json``` format also.
  
Example,
```
{
  "input": {
    "user": "shahidul",
    "operation": "write"
  }
}
```
By the input example above, we're provably asking a question, ``` Is user Shahidul allowed to invoke GET /protected/resource ```.


  

- https://www.openpolicyagent.org/docs/v0.12.2/kubernetes-admission-control/
- https://www.youtube.com/watch?v=UN0su8fdGcs

WIth tektoncd: https://docs.google.com/document/d/1pH9wyVaGVLjnhi5tOa2TSq7d1j5HTTeCbCmosRo4jWE/edit

official doc: https://www.openpolicyagent.org/docs/latest/
Opa and constest: https://garethr.dev/2019/06/introducing-conftest/

Installation: https://www.openpolicyagent.org/docs/v0.12.2/kubernetes-admission-control/
