## Samples are in the process of being migrated to http://docs.particular.net/samples/

# NServiceBus.Msmq.Samples #
----------

This repository contains the Samples for the MSMQ transport.
 
##Error Handling 

This sample demonstrates what happens when exceptions occur when messages are handled and how retries work. As a comparison, it also illustrates the behavior when the Second Level Retries (SLR) feature is turned off.

##Gateway

This sample demonstrates how logically different sites such as Headquarters, Stores communicate using the NServiceBus Gateway feature. This sample also demonstrates the use of the DataBus feature which enables in transferring large data. Data that needs to be transferred using the databus is defined using the DataBusProperty<T> as shown in Headquarter.Messages.PriceUpdated and the Headquarter endpoint has initialization code to setup the Databus.

##VideoStore

This sample implements the following worflow of a fictional video store. Users can order videos from the website. Once orders are submitted, there is a window of time allocated for handling cancellations due to buyer's remorse. Once the order has been accepted, they are provisioned and made available for download. In implementing the above workflow various aspects are highlighted:


- The Sales endpoint illustrates the use of the Saga pattern to handle the buyer's remorse scenario.  
The CustomerRelations endpoint illustrates how in-memory events (domain events pattern) can be defined and subscribed to.

- The request/response pattern is illustrated for the video provisioning between the ContentManagement endpoint and the Operations Endpoint.
The ECommerce endpoint is implemented as an ASP.NET MVC4 application which uses SignalR to show feedback to the user. 

- This sample also illustrates the use of Unobtrusive message conventions to let NServiceBus know in order to identify commands, events and messages defined as POCOs which avoids having to add a reference to the NServiceBus libraries in the message definition dlls.

- The use of message headers and message mutator is also illustrated when the user clicks on the Check box on the ECommerce web page, which conveniently stops at the predefined breakpoints in the message handler code on the endpoints.

- The use of encryption is illustrated by passing in the Credit Card number and the Expiration date from the ECommerce web site. The UnobtrusiveConventions defined in the ECommerce endpoint show how to treat certain properties as encrypted. Both the ECommerce and the Sales endpoint is setup for RijndaelEncryption and the encryption key is provided in the config file. If the messages are inspected in the queue, both the Credit Card number and the Expiration Date will show the encrypted values.  
