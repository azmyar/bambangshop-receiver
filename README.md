# BambangShop Receiver App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a Rocket web framework skeleton that you can work with.

As this is an Observer Design Pattern tutorial repository, you need to implement a feature: `Notification`.
This feature will receive notifications of creation, promotion, and deletion of a product, when this receiver instance is subscribed to a certain product type.
The notification will be sent using HTTP POST request, so you need to make the receiver endpoint in this project.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Receiver" folder.

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    ROCKET_PORT=8001
    APP_INSTANCE_ROOT_URL=http://localhost:${ROCKET_PORT}
    APP_PUBLISHER_ROOT_URL=http://localhost:8000
    APP_INSTANCE_NAME=Safira Sudrajat
    ```
    Here are the details of each environment variable:
    | variable                | type   | description                                                     |
    |-------------------------|--------|-----------------------------------------------------------------|
    | ROCKET_PORT             | string | Port number that will be listened by this receiver instance.    |
    | APP_INSTANCE_ROOT_URL   | string | URL address where this receiver instance can be accessed.       |
    | APP_PUUBLISHER_ROOT_URL | string | URL address where the publisher instance can be accessed.       |
    | APP_INSTANCE_NAME       | string | Name of this receiver instance, will be shown on notifications. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)
3.  To simulate multiple instances of BambangShop Receiver (as the tutorial mandates you to do so),
    you can open new terminal, then edit `ROCKET_PORT` in `.env` file, then execute another `cargo run`.

    For example, if you want to run 3 (three) instances of BambangShop Receiver at port `8001`, `8002`, and `8003`, you can do these steps:
    -   Edit `ROCKET_PORT` in `.env` to `8001`, then execute `cargo run`.
    -   Open new terminal, edit `ROCKET_PORT` in `.env` to `8002`, then execute `cargo run`.
    -   Open another new terminal, edit `ROCKET_PORT` in `.env` to `8003`, then execute `cargo run`.

## Mandatory Checklists (Subscriber)
-   [x] Clone https://gitlab.com/ichlaffterlalu/bambangshop-receiver to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [x] Commit: `Create Notification model struct.`
    -   [x] Commit: `Create SubscriberRequest model struct.`
    -   [x] Commit: `Create Notification database and Notification repository struct skeleton.`
    -   [x] Commit: `Implement add function in Notification repository.`
    -   [x] Commit: `Implement list_all_as_string function in Notification repository.`
    -   [x] Write answers of your learning module's "Reflection Subscriber-1" questions in this README.
-   **STAGE 3: Implement services and controllers**
    -   [x] Commit: `Create Notification service struct skeleton.`
    -   [x] Commit: `Implement subscribe function in Notification service.`
    -   [x] Commit: `Implement subscribe function in Notification controller.`
    -   [x] Commit: `Implement unsubscribe function in Notification service.`
    -   [x] Commit: `Implement unsubscribe function in Notification controller.`
    -   [x] Commit: `Implement receive_notification function in Notification service.`
    -   [x] Commit: `Implement receive function in Notification controller.`
    -   [x] Commit: `Implement list_messages function in Notification service.`
    -   [x] Commit: `Implement list function in Notification controller.`
    -   [x] Write answers of your learning module's "Reflection Subscriber-2" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Subscriber) Reflections

#### Reflection Subscriber-1

1. In this tutorial, we chose to use RwLock<> to synchronize access to the Vec of Notifications because it suits the needs of the class where there will be multiple threads performing concurrent reads on the Vec. RwLock<> is a more suitable choice than Mutex<> because of its flexibility in managing Read/Write access. RwLock<> allows multiple readers or a single writer at the same time. This advantage is not possessed by Mutex<>, which only allows one thread to perform either reading or writing and implements locking for other threads. Therefore, in this context, RwLock<> is considered more effective.

2. In Rust, static variables and constants behave similarly, where both are read-only after initialization. This is part of Rust's effort to prioritize safety in multi-threading by limiting access to mutable data from multiple threads simultaneously. The purpose of this limitation is to prevent race condition and data race issues that can cause unexpected program behavior. As a solution, Rust allows mutation of data on static variables using immutable data structures, but still introduces locking mechanisms like RwLock and Mutex. Thus, data mutation can be done safely and coordinatedly.

#### Reflection Subscriber-2

1. After completing this module, I became interested in understanding the roles of various files not extensively explained in the tutorial. For example, I found that Cargo.toml acts as the main configuration file for a Rust project, allowing management of dependencies, project configuration, and clear definition of project metadata. Additionally, there is Rocket.toml, primarily used for specific Rocket framework configurations, such as server port settings, thread count, and logging level, but in this tutorial, it is only used to set the IP address and server port. Furthermore, lib.rs proved to be a file rich in main application configurations, including definition of global variables, basic application configuration structure, error handling, and usage of HTTP clients in the context of a Rust application using Rocket and requests.

2. From this module, I realized that the Observer pattern can be a practical solution for handling the addition of more subscribers. This occurs due to the clear separation between Publisher and Observer, as well as message management between data owner and subscribers. However, adding subscribers to the system can increase code complexity and make the process not as immediate as when there is only one main application instance. Nevertheless, the benefits gained from flexibility and scalability can provide significant added value to the application.

3. I have recently started exploring both of these features in Postman. Although I have not fully mastered the syntax of creating testing scripts, I have successfully implemented some testing scripts that I found from the internet. I found this feature very useful in conducting automated testing when testing server responses. Additionally, I also explored the API documentation feature in Postman by adding clear descriptions to each request. This allows me to see examples of the request body needed to call each request more efficiently.