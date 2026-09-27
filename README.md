# CST8915 Lab 1: Algonquin Pet Store on Azure VM

**Student Name**: Pearl Williams-Cox  

**Student ID**: 040926099 

**Course**: CST8915 Full-stack Cloud-native Development  

**Semester**: Fall 2026

---

## Demo Video

🎥 [Watch Demo Video](YOUTUBE-LINK-HERE)

---

## Technical Explanations

### Order Service (Node.js)

The Order Service is responsible for receiving orders from the Store Front and sending them to RabbitMQ. It is built using Node.js and runs on port 3000. When a customer selects a product and places an order, the Store Front sends the order information to this service. During the lab, I tested the service directly with a POST request and received an "Order received" response.

In the microservices architecture, the Order Service acts as the connection between the Store Front and RabbitMQ. Instead of the Store Front communicating directly with RabbitMQ, it sends the order to the Order Service, which then places the message into the RabbitMQ `order_queue`. This keeps the responsibilities of each service separate. I verified this by placing an order through the Store Front and checking that the number of messages in the RabbitMQ queue increased.

### Product Service (Rust)

The Product Service is responsible for providing the product information used by the Store Front, including the product IDs, names, and prices. It is written in Rust and runs on port 3030. In this lab, I started the service using `cargo run` and tested the `/products` endpoint with curl. It returned the three products used by the application: Dog Food, Cat Food, and Bird Seeds.

In the microservices architecture, the Product Service handles the product catalog separately from the other parts of the application. The Store Front sends a request to the Product Service to retrieve the available products and then displays them to the user. This means the Store Front does not need to contain or manage the product data itself. I verified the communication was working when the products and their prices successfully appeared in the Store Front running on my Azure VM.

### Store Front (Vue.js)

The Store Front is the customer-facing part of the application where users can view products, select a product, enter a quantity, see the total price, and place an order. It is built with Vue.js and runs on port 8080. For the Azure deployment, I configured the Store Front to use my VM's public IP when communicating with the Product Service and Order Service instead of using localhost.

In the microservices architecture, the Store Front acts as the user interface while the other services handle the backend work. It retrieves the product list from the Product Service on port 3030 and sends submitted orders to the Order Service on port 3000. I tested this by selecting two units of Dog Food, which correctly calculated a total of $39.98, and then placing the order successfully.

---

## Challenges and Learnings

One challenge I ran into during this lab was connecting to the Azure VM after I no longer had access to the original SSH private key. I learned how important it is to keep SSH keys somewhere safe because the original private key cannot simply be downloaded again. I was able to restore access by adding a new SSH public key to the VM and then reconnecting through VS Code Remote SSH.

I also learned a lot about how the different parts of a microservices application communicate. Before this lab, it was harder for me to picture how separate services could work together as one application. Testing each service individually and then seeing the Store Front load products, send an order to the Order Service, and have that order appear in RabbitMQ made the overall architecture much easier for me to understand.

---

## Acknowledgments

This project was completed using the starter code and lab instructions provided for CST8915 Full-stack Cloud-native Development.
