---
id: Hexagonal architecture pattern
aliases: []
tags:
  - architect
category: Tech
date: 2024-10-20
published: 2024-10-20
title: Hexagonal architecture pattern
---


## Intent

The hexagonal architecture pattern, which is also known as the ports and adapters pattern, was proposed by Dr. Alistair Cockburn in 2005. It aims to create loosely coupled architectures where application components can be tested independently, with no dependencies on data stores or user interfaces (UIs). This pattern helps prevent technology lock-in of data stores and UIs. This makes it easier to change the technology stack over time, with limited or no impact to business logic. In this loosely coupled architecture, the application communicates with external components over interfaces called _ports_, and uses _adapters_ to translate the technical exchanges with these components.

## Motivation

The hexagonal architecture pattern is used to isolate business logic (domain logic) from related infrastructure code, such as code to access a database or external APIs. This pattern is useful for creating loosely coupled business logic and infrastructure code for AWS Lambda functions that require integration with external services. In traditional architectures, a common practice is to embed business logic in the database layer as stored procedures and in the user interface. This practice, along with using UI-specific constructs within business logic, leads to closely coupled architectures that cause bottlenecks in database migrations and user experience (UX) modernization efforts. The hexagonal architecture pattern enables you to design your systems and applications by purpose rather than by technology. This strategy results in easily exchangeable application components such as databases, UX, and service components.

## Applicability

Use the hexagonal architecture pattern when:

- You want to decouple your application architecture to create components that can be fully tested.
    
- Multiple types of clients can use the same domain logic.
    
- Your UI and database components require periodical technology refreshes that don't affect application logic.
    
- Your application requires multiple input providers and output consumers, and customizing the application logic leads to code complexity and lack of extensibility.
    

## Issues and considerations

- **Domain-driven design**: Hexagonal architecture works especially well with domain-driven design (DDD). Each application component represents a sub-domain in DDD, and hexagonal architectures can be used to achieve loose coupling among application components.
    
- **Testability**: By design, a hexagonal architecture uses abstractions for inputs and outputs. Therefore, writing unit tests and testing in isolation become easier because of the inherent loose coupling.
    
- **Complexity**: The complexity of separating business logic from infrastructure code, when handled carefully, can bring great benefits such as agility, test coverage, and technology adaptability. Otherwise, issues can become complex to solve.
    
- **Maintenance overhead**: The additional adapter code that makes the architecture pluggable is justified only if the application component requires several input sources and output destinations to write to, or when the inputs and output data store has to change over time. Otherwise, the adapter becomes another additional layer to maintain, which introduces maintenance overhead.
    
- **Latency issues**: Using ports and adapters adds another layer, which might result in latency.
    

## Implementation

Hexagonal architectures support the isolation of application and business logic from infrastructure code and from code that integrates the application with UIs, external APIs, databases, and message brokers. You can easily connect business logic components to other components (such as databases) in the application architecture through ports and adapters.

Ports are technology-agnostic entry points into an application component. These custom interfaces determine the interface that allows external actors to communicate with the application component, regardless of who or what implements the interface. This is similar to how a USB port allows many different types of devices to communicate with a computer, as long as they use a USB adapter.

Adapters interact with the application through a port by using a specific technology. Adapters plug into these ports, receive data from or provide data to the ports, and transform the data for further processing. For example, a REST adapter enables actors to communicate with the application component through a REST API. A port can have multiple adapters without any risk to the port or to the application component. To extend the previous example, adding a GraphQL adapter to the same port provides an additional means for actors to interact with the application through a GraphQL API without affecting the REST API, the port, or the application.

Ports connect to the application, and adapters serve as a connection to the outside world. You can use ports to create loosely coupled application components, and exchange dependent components by changing the adapter. This enables the application component to interact with external input and outputs without needing to have any contextual awareness. Components are exchangeable at any level, which facilitates automated testing. You can test components independently without any dependencies on the infrastructure code instead of provisioning an entire environment to conduct testing. The application logic doesn't depend on external factors, so testing is simplified and it becomes easier to mock dependencies.

For example, in a loosely coupled architecture, an application component should be able to read and write data without knowing the details of the data store. The responsibility of the application component is to supply data to an interface (port). An adapter defines the logic of writing to a data store, which can be a database, a file system, or an object storage system such as Amazon S3, depending on the application's needs.

### High-level architecture

The application or application component contains the core business logic. It receives commands or queries from the ports, and sends requests out through the ports to external actors, which are implemented through adapters, as illustrated in the following diagram.

![Hexagonal architecture pattern](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/cloud-design-patterns/images/hexagonal-1.png)

### Implementation using AWS services

AWS Lambda functions often contain both business logic and database integration code, which are tightly coupled to meet an objective. You can use the hexagonal architecture pattern to separate business logic from infrastructure code. This separation enables unit testing of the business logic without any dependencies on the database code, and improves the agility of the development process.

In the following architecture, a Lambda function implements the hexagonal architecture pattern. The Lambda function is initiated by the Amazon API Gateway REST API. The function implements business logic and writes data to DynamoDB tables.

![Implementing the hexagonal architecture pattern on AWS](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/cloud-design-patterns/images/hexagonal-2.png)

### Sample code

The sample code in this section shows how to implement the domain model by using Lambda, separate it from infrastructure code (such as the code to access DynamoDB), and implement unit testing for the function.

#### Domain model

The domain model class has no knowledge of external components or dependencies—it only implements the business logic. In the following example, the class `Recipient` is a domain model class that checks for overlaps in the reservation date.

```python
class Recipient:
    def __init__(self, recipient_id:str, email:str, first_name:str, last_name:str, age:int):
        self.__recipient_id = recipient_id
        self.__email = email
        self.__first_name = first_name
        self.__last_name = last_name
        self.__age = age
        self.__slots = []
 
    @property
    def recipient_id(self):
        return self.__recipient_id
    #.....     
 
    def are_slots_same_date(self, slot:Slot) -> bool:
        for selfslot in self.__slots:
            if selfslot.reservation_date == slot.reservation_date:
                return True        
        return False
 
    def is_slot_counts_equal_or_over_two(self) -> bool:
    #.....
```


#### Input port

The `RecipientInputPort` class connects to the recipient class and runs the domain logic.

```python
class RecipientInputPort(IRecipientInputPort):
    def __init__(self, recipient_output_port: IRecipientOutputPort, slot_output_port: ISlotOutputPort):
        self.__recipient_output_port = recipient_output_port
        self.__slot_output_port = slot_output_port

    '''
    make reservation: adapting domain model business logic
    '''
    def make_reservation(self, recipient_id:str, slot_id:str) -> Status:
        status = None        
        
        # ---------------------------------------------------
        # get an instance from output port
        # ---------------------------------------------------
        recipient = self.__recipient_output_port.get_recipient_by_id(recipient_id)
        slot = self.__slot_output_port.get_slot_by_id(slot_id)

        if recipient == None or slot == None:
            return Status(400, "Request instance is not found. Something wrong!")

        print(f"recipient: {recipient.first_name}, slot date: {slot.reservation_date}")

        # ---------------------------------------------------
        # execute domain logic
        # ---------------------------------------------------
        ret = recipient.add_reserve_slot(slot)

        # ---------------------------------------------------
        # persistent an instance throgh output port
        # ---------------------------------------------------
        if ret == True:
            ret = self.__recipient_output_port.add_reservation(recipient)

        if ret == True:
            status = Status(200, "The recipient's reservation is added.")
        else:
            status = Status(200, "The recipient's reservation is NOT added!")
        return status
```

#### DynamoDB adapter class

The `DDBRecipientAdapter` class implements access to the DynamoDB tables.

```python
class DDBRecipientAdapter(IRecipientAdapter):
    def __init__(self):
        ddb = boto3.resource('dynamodb')
        self.__table = ddb.Table(table_name)
 
    def load(self, recipient_id:str) -> Recipient:
        try:
            response = self.__table.get_item(
                Key={'pk': pk_prefix + recipient_id})
      　... 
 
    def save(self, recipient:Recipient) -> bool:
        try:
            item = {
                "pk": pk_prefix + recipient.recipient_id,
                "email": recipient.email,
                "first_name": recipient.first_name,
                "last_name": recipient.last_name,
                "age": recipient.age,
                "slots": []
            }
          # ... 
```

The Lambda function `get_recipient_input_port` is a factory for instances of the `RecipientInputPort` class. It constructs instances of output port classes with related adapter instances.

```python
def get_recipient_input_port():
    return RecipientInputPort(
        RecipientOutputPort(DDBRecipientAdapter()), 
        SlotOutputPort(DDBSlotAdapter()))
 
def lambda_handler(event, context):

    body = json.loads(event['body'])
    recipient_id = body['recipient_id']
    slot_id = body['slot_id']
 
    # get an input port instance
    recipient_input_port = get_recipient_input_port()
    status = recipient_input_port.make_reservation(recipient_id, slot_id)
 
    return {
        "statusCode": status.status_code,
        "body": json.dumps({
            "message": status.message
        }),
    }
```

#### Unit testing

You can test the business logic for domain model classes by injecting mock classes. The following example provides the unit test for the domain model `Recipent` class.

```python
def test_add_slot_one(fixture_recipient, fixture_slot):
    slot = fixture_slot
    target = fixture_recipient
    target.add_reserve_slot(slot)
    assert slot != None
    assert target != None
    assert 1 == len(target.slots)
    assert slot.slot_id == target.slots[0].slot_id
    assert slot.reservation_date == target.slots[0].reservation_date
    assert slot.location == target.slots[0].location
    assert False == target.slots[0].is_vacant
 
def test_add_slot_two(fixture_recipient, fixture_slot, fixture_slot_2):
    #.....
 
def test_cannot_append_slot_more_than_two(fixture_recipient, fixture_slot, fixture_slot_2, fixture_slot_3):
    #.....
 
def test_cannot_append_same_date_slot(fixture_recipient, fixture_slot):
    #.....
```

#### GitHub repository

For a complete implementation of the sample architecture for this pattern, see the GitHub repository at [https://github.com/aws-samples/aws-lambda-domain-model-sample](https://github.com/aws-samples/aws-lambda-domain-model-sample).

## Related content

- [Hexagonal architecture](https://alistair.cockburn.us/hexagonal-architecture/), article by Alistair Cockburn
    
- [Developing evolutionary architectures with AWS Lambda](https://aws.amazon.com/jp/blogs/news/developing-evolutionary-architecture-with-aws-lambda/) (AWS blog post in Japanese)
