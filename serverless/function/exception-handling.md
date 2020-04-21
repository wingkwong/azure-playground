# Exception Handling

Azure Functions runtime will 
- capture the exception and will retr calling the function 5 times including the first call
- receive up to 16 messages and run functions for each in parallel
- ges another batch of 16 and processes those when the number being processed gets down to 8

