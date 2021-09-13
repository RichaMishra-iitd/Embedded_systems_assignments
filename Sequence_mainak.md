```mermaid
sequenceDiagram
    participant Customer
		participant Customer_interface
    participant Central_dispatcher
		participant Kitchen_server
		participant Driver_server
		participant Tea_seller
		participant Driver
		 loop Every m minute
        Tea_seller->>Kitchen_server: Number of hot tea
    end
		loop Every m minute
        Driver->>Driver_server: Updates Status
		Note over Driver,Driver_server: location updates
    end
	

	Customer ->> Customer_interface: login
	activate Customer
	activate Customer_interface
	alt details_correct
        Customer_interface -->> Customer: accepted 
    else details_incorrect
        Customer_interface -->> Customer: rejected
    end
	
	
	
	
	Customer->>Customer_interface: Purchase order n cup
	Customer_interface->>Central_dispatcher: number of items
	activate Central_dispatcher
	Central_dispatcher-->>Customer_interface: return
	deactivate Central_dispatcher
	Customer_interface-->>Customer: order accepted
	Customer_interface->>Customer: Payment requested
	Customer-->>Customer_interface: clears all dues
	
	
	deactivate Customer
	deactivate Customer_interface
	

	Central_dispatcher->>Kitchen_server: allocates seller
	activate Central_dispatcher
	activate Kitchen_server
 Kitchen_server->>Tea_seller: informs number of items to pack
 activate Tea_seller

 
        Tea_seller-->>Kitchen_server: accepted 
		deactivate Tea_seller
			Kitchen_server-->>Central_dispatcher: location of the seller
			deactivate Kitchen_server
			deactivate Central_dispatcher



Central_dispatcher->>Driver_server: allocates driver
activate Driver_server
activate Central_dispatcher
	Driver_server->>Driver: informs locations
 activate Driver
        Driver-->>Driver_server: accepted 
    deactivate Driver
	Driver_server-->>Central_dispatcher:information of the driver
deactivate Driver_server
	deactivate Central_dispatcher

	loop every k minute
	
	Driver_server->>Customer_interface: Location information

end

	
	

	Driver->>Tea_seller: arrives at location
	
	activate Driver
	activate Tea_seller
	Tea_seller-->>Driver: order delivered
	deactivate Tea_seller
	Driver->>Customer: Delivery
	activate Customer
	deactivate Driver
	
	
	
	
	
	
	
	
	
	

	alt tea hot 
	activate Customer_interface
        Customer-->>Customer_interface: accepts order
		
    else tea cold
        Customer-->>Customer_interface: rejects order
					

    end
	deactivate Customer_interface
	deactivate Customer
	
	
 
