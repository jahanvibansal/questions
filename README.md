1. Describe experience resume latest project
2. What is Apache Kafka topic? Partition and how message is stored?
3. Error Handling? Try Catch block
4. Using version control to push changes
5. How would I prioritize tickets assigned to me? Bugfix vs Devwork?
6. Production issue where there is 100% CPU utilization what would you do to fix it?
7. Spring annotation where I used it?
8. @Service and @Component
9. Junit and Mockito framework what are they?
10. How I used Splunk logs?
11. Retrys in KafkaPublisher
12. Consumer/Client end to end business logic
13. How I went through the SDLC? What I think my responsibilities would be as a Senior Developer.

/**
 * Our company has recently purchased a Vending Machine hardware with the following features. We need
 * to develop a software to work with its API.
 *
 * VM Hardware has on/off, dispense, up,and down button
 * VM Hardware has a three-lines display
 * VM Hardware has creditCard reader with an API method "process" that accepts two callbacks(succeed, failed)
 * ( assumption: if the payment is "on" it is a success otherwise failure )
 *
 * Requirements:
 * VM can return status of the machine ON/OFF/OUT_OF_ORDER
 * OUT_OF_ORDER: When there is no product in the inventory
 * VM shows nothing on display when its off
 * VM shows "Welcome" message on line 1, "Select an options" on line 2 on start
 * VM shows one item at a time with up/down button on line 2 (list is cyclic)
 * VM shows "Sold Out" when no product is available
 * VM shows "Sold Out" for each item sold with quantity 0
 ** VM dispense product upon payment successful transaction
 ** VM dispense 1 product at a time per each payment
 ** VM shows "Payment failed" on payment failure
 ** VM shows "Please wait..." on line 3 while payment is in progress
 ** VM will reset by any key after payment transaction (failed or succeed)

 * VM can show total received money
 * VM can show total sold products
 * VM inventory cannot be negative
 * <p>
 * <p>
 * Enhance SnackVendingMachine with the following inventory.
 * ("Coke", 1.35, 2);
 * ("Gum", 2.25, 4);
 * ("Chocolate", 3.50, 3);
 *
 * Note:
 * - If any of the requirements is not clear, make and document your assumption.
 * - Modularization and Clean code is important
 * - This assignment, must be done TDD approach.
 * -
 */
 
import java.util.*;
import java.io.*;

class Main {
public static void main(String[] args) {
      

VendingMachine vm = new VendingMachine();
System.out.println(vm.getStatus());
HashMap<String,HashMap<Integer,Integer>> inventory = vm.getInventory();
System.out.println(inventory.size());
vm.addProduct("Coke", 2, 24);
System.out.println(inventory.size());
}
}
class VendingMachine{
  public String status;
  HashMap<String, HashMap<Integer,Integer>> inventory;

  public VendingMachine(){
    this.status = "OUT_OF_ORDER";
     inventory = new HashMap<>();
  }

  public String getStatus(){
    return this.status;
  }
  public HashMap<String,HashMap<Integer,Integer>> getInventory(){
    return this.inventory;
  }

  public void addProduct(String productName, Integer productPrice, Integer productQuantity){
      HashMap<Integer,Integer> product = new HashMap<>();
      product.put(productPrice,productQuantity);
      inventory.put(productName,product);
  }

    

}
1.	KMS API: what is envelope encryption? Benefits of envelope encryption
2.	HTTP compression: how to enable in spring boot
3.	Valve logging attribute setpattern, setsufix, setoption,setrule
4.	AWS autoscaling mechanism
5.	AWS immutable infratructure 
6.	Singleton pattern
7.	Continuous delivery (true/false ): package and dependencies -> same environment, testing become mundane, 
8.	Full authentication is required to access this resource. How to fix? pick the following
a.	get password from logging
b.	get username and password from logging
c.	diable security management.security.enable = true/flase
9.	Java Reflect: methods, their return type, and their parameter 
a.	getmethod()
b.	invoke()
10.	ClientBuilder and Webtarget: fill code to match API endpoint and invoke correct HTTP method
11.	Amazon Load Balancer: load balancer route request to any cloud providers/within availability zone/within AWS ...
a.	name one load balancer: ELB
b.	application load balancer 	
12.	Coding: remove vowels in a string
1. Runtime polymorphism
	overriding method
	same name, same parameter
	same or subclass (covariant) of return type
	same or more accessibility
			
2. Singleton
	private constructor of object 
	private static class instance
	static method which check for class instance 
		if null instance = new constructor() 
		return instance 

3. Tomcat logging: 
	Server logging config: server.xml
	Create a file called log4j.properties with the following content and save it into $CATALINA_HOME/lib.
		
	
log4j.rootLogger=INFO, R 
log4j.appender.R=org.apache.log4j.RollingFileAppender 
log4j.appender.R.File=${catalina.base}/logs/tomcat.log 
log4j.appender.R.MaxFileSize=10MB 
log4j.appender.R.MaxBackupIndex=10 
log4j.appender.R.layout=org.apache.log4j.PatternLayout 
log4j.appender.R.layout.ConversionPattern=%p %t %c - %m%n
          

		
	Download Log4J (v1.2 or later) and place the log4j jar in $CATALINA_HOME/lib.
	Build or download the additional logging components. See the extras components documentation for details.
	Replace $CATALINA_HOME/bin/tomcat-juli.jar with output/extras/tomcat-juli.jar.
	Place output/extras/tomcat-juli-adapters.jar in $CATALINA_HOME/lib.
	Delete $CATALINA_BASE/conf/logging.properties to prevent java.util.logging generating zero length log files.
	Start Tomcat

4. ClientBuilder and webtarget 
	Client client = ClientBuilder.newBuilder()
                             .property("connection.timeout", 100)
                             .sslContext(sslContext)
                             .register(JacksonJsonProvider.class)
                             .build();
	WebTarget target = client.target("http://commerce.com/customers/{id}")
                         .resolveTemplate("id", "123")
                         .queryParam("verbose", true);
	
	Response response = client.target("http://commerce.com/customers/123")
                          .accept("application/json")
                          .get();
	Customer customer = client.target("http://commerce.com/customers/123")
                          .accept("application/json")
                          .get(Customer.class);
						  
	Response response = client.target("http://commerce.com/customers")
                          .request().
                          .post(Entity.json(customer));
	
	
5. Spring AOP: jointpoint -> getSignature().getName()
				     (around advice) processingJointPoint
					 .proceed()

6. Validation: fill-in code 

	Annotation-based
		JSR: @Min, @Max, @NotNull, @Size(min=,max=), @Email.. 
		@NotEmpty ( String, Collection, Map or Array), @NotBlank(text), @Positive, @Negative
		@Valid
	
	Customized validator: 
		support() indicate class to perform validation
		validate() perform validation of fields 
		new UserValidator().validate(user, bindingResult);
		 
	Common parameter: (message="") - message is rendered when validation fails 
	bindingResult.hasErrors()	
	

7. AWS scaling:
	what threshhold: for RDS it's memory 20GiB
	what service to scale: 
		EC2: number of Amazon EC2 instances available to handle the load for your application
		Application: AWS resources
		AWS auto scaling: multiple resources across multiple serivces 
	Policies:
	target: tracking scaling policies, you select a metric and set a target value
	step: target tracking scaling policies, you select a metric and set a target value
	schedule: scale at a date and time 
	
	Strategies: 
	Optimize for availability—AWS Auto Scaling scales the resource out and in automatically to maintain resource utilization at 40 percent.
	Balance availability and cost—AWS Auto Scaling scales the resource out and in automatically to maintain resource utilization at 50 percent. 
	Optimize for cost—AWS Auto Scaling scales the resource out and in automatically to maintain resource utilization at 70 percent.
8. AWS SQS: 
	AmazonSQS sqs = AmazonSQSClientBuilder.defaultClient();
	CreateQueueRequest createQueueRequest = new CreateQueueRequest("MyQueue");
    String myQueueUrl = sqs.createQueue(createQueueRequest).getQueueUrl();

	sqs.sendMessage(new SendMessageRequest(myQueueUrl, "This is my message text
	
	ReceiveMessageRequest receiveMessageRequest = new ReceiveMessageRequest(myQueueUrl);
    List<Message> messages = sqs.receiveMessage(receiveMessageRequest).getMessages();

	sqs.deleteMessage(new DeleteMessageRequest(myQueueUrl, message.getReceiptHandle()));

	delay queue: give consumer more time to process the message
	standard queue (duplication,unlimited)
	fifo queue (no duplication, 300 tps, maintain order)
	dead-letter queue: debugging, isolate messages that are failed to be delivered for further analysis. 
		Set up alarm if a message is sent to dead-letter queue
		
9. Serialization and Deserialization 
	fileOuputStream(filepath), fileInputStream(filepath)
	objectOutputStream(fos), objectInputStream(fis)
	oos.writeObject(), (castObject) ois.readObject()

10. Actuator: /trace endpoint
	@Repository
	public class CustomTraceRepository extends InMemoryTraceRepository {

		private static final Logger log = LoggerFactory.getLogger(CustomTraceRepository.class);

		public CustomTraceRepository() {
			super.setCapacity(200);
		}
    }

What collections you have used in the project?
Why you use hash map.
Where you use hash map.
Why you choose to use hashmap to avoid duplicate, not other collections like hash set in your project.
In the project, you use the hashmap, what you set as a key and what you set as a value.
Can we use object as a key in the hash set?
What will happen if it generate the same hashcode when we store the key-value pair in the hashmap.
Can we override the hashcode method.
If we have a list of employee, how we can customize the sorting function by the combination of lastname and firstname
We have two arrayList, contains Integers, how we can find the unique number of this two array and how can we find the common number of these two array(can not use hashmap and hashset)
How you use multithreading in the project, and if there are multiple API call, how you handle it.

So In the project, the database will update everday, what can you do to check which row has been updated.

Where did you use java8 in your project, why you use java8 here not java7.
How do you identify if two file have the same content in unix.
What annotation of spring framework you used in your project.

-	Tell me about the recent project
-	What is and why do we need Eureka Server
-	Why Eureka Server is called Discovery Server
-	MongoDB ?
-	Reactive Approach ?
-	How to make a thread class
-	Rest API vs SOAP
-	Http method (Get Post Put Delete)
-	Kafka?
-	Java EE, Spring
-	Is Singleton ThreadSafe?
-	How do I make Singleton to be thread safe?
-	Interviewer introduced a project they are working now and asked if I’m interested

