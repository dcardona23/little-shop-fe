# Little Shop  

[Little Shop GitHub Repo](https://github.com/dcardona23/little-shop-fe-final-starter)

[Danielle Cardona LinkedIn](https://github.com/dcardona23/little-shop-fe-final-starter)

### Abstract:
Building off a previous group project, I developed a coupon management system with a Ruby on Rails backend API. The application allows merchants to create, activate, and deactivate coupons, and begins mapping out the functionality to apply coupons to merchant invoices. The system solves the problem of complex coupon management for e-commerce platforms by providing a robust API for coupon operations, including filtering, activation rules, and usage tracking. 

### Installation Instructions:
- Clone the repository
- Navigate to the project directory: cd coupon-project
- Install dependencies: bundle install
- Set up the database: rails db:create db:migrate
- Start the Rails server: rails server
- The API will be available at: http://localhost:3000

### Preview of App:
![Little Shop GIF](https://videoapi-muybridge.vimeocdn.com/animated-thumbnails/image/36128a8f-23cc-4724-9866-ded27eacdb6c.gif?ClientID=sulu&Date=1731454863&Signature=11c26968097ee6175740a33801f4701a1f31309c) 

### Context:
(Give some context for the project here. How long did you have to work on it? What specific work/improvements did you contribute to this FE application?)

### Learning Goals:
- Write migrations to create tables and relationships between tables
- Implement CRUD functionality for a resource
- Use MVC to organize code effectively, limiting the amount of logic included in serializers and controllers
- Use built-in ActiveRecord methods to join tables of data, make calculations, and group data based on one or more attributes
- Write model tests that fully cover the data logic of the application
- Write request tests that fully cover the functionality of the application
- Display data for users in a frontend application by targeting DOM elements

### Wins + Challenges:
Wins
- I was able to implement strong validation logic for coupons. For example, the code ensures that either dollar_off or percent_off is present, but not both, and imposes a unique constraint on coupon codes to ensure data integrity and consistency. Similarly, I was able to implement functionality to prevent merchants from deactivating coupons with pending invoices to prevent inadvertently overcharging customers.
- The project adheres to the single responsibility principle and encapsulates business logic in the Coupon model, including the save_coupon and activate/deactivate methods. This allows the controller to focus on the HTTP request/response cycle and makes the code easier to maintain and test.

Challenges 
- One of the unexpected challenges I encountered was accidentally deleting the routes file while making changes to the application's configuration. This resulted in the loss of all defined routes, which caused the application to break and return routing errors when trying to access endpoints. To address this issue, I first identified the missing routes by checking the logs and trying to access different parts of the application. I then restored the routes file from version control, but I also had to go back through the code to ensure that the correct routes were in place for the CouponsController and other API endpoints. This experience highlighted the importance of being extra cautious when working with configuration files, particularly routes, as they are essential for directing requests to the appropriate controller actions. 
- One of the most complex pieces of logic in this project involved the activation and deactivation of coupons, specifically the rules around limiting a merchant to only having five active coupons and preventing deactivation if there are any associated "packaged" invoices.The logic required to ensure that a coupon can only be activated if the merchant has fewer than five active coupons was tricky. It needed to account for multiple conditions: checking if the coupon was already active, ensuring that the merchant didn’t exceed the limit, and verifying that the coupon could actually be activated. Additionally, the deactivation process became more complicated when invoices using the coupon were involved, as I had to craft logic to check the status of each invoice to prevent deactivation of packaged invoices. To overcome this challenge, I ensured that all coupon activation and deactivation logic was wrapped in clear conditionals, and used database queries to validate the merchant's active coupon count and check invoice statuses. Although it added complexity, this approach helped maintain the business rules and prevented unintended behaviors. 