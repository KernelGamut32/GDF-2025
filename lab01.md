# Lab 01 - Create an Agent for Renting a Car

* In an incognito browser, navigate to https://app.pluralsight.com
* Log in using the email and password provided to you
* In the upper left, make sure that "Skills" is selected - there is a dropdown that you can click to change if needed
* Click "Hands-on" and under "Cloud Sandboxes" click "Get Started"
* You may see an error: "There was a problem loading your playgrounds"; you can safely ignore
* Under "Google Cloud Sandbox", click "Open Sandbox"
* Click the "Start Sandbox" button
* Right-click the "Open Sandbox" button and open the link in a new tab
* Email address should be populated already in the Sign In window; if not, you can copy from the sandbox details screen
* Click "Next"
* For password, copy/paste the password provided to you in the sandbox details screen
* Click "Next"
* If presented with the welcome message, click the "I understand" button
* In the "Welcome" dialog, make sure "United States" is selected under Country and click the checkbox next to "I agree"; click "Agree and Continue"
* From the same incognito session, in a separate tab, navigate to https://dialogflow.cloud.google.com/cx
* In the "Select Project" dialog, click "All"
* Choose the project with the name starting with "playground"
* You should be prompted with a dialog asking you if you want to enable the "DialogFlow API"; click "Enable API"
* Click the "Create agent" button
* Click "Build your own"
* For "Display name", enter "Car rental", select "global" for the "Location", leave all other settings at the defaults, and click "Create"
* Modify the default start page
    - Click on "Start Page"
    - Click "Default Welcome intent"
    - Scroll down to "Agent responses" under "Fulfillment"
    - In "Agent dialogue", add a new welcome message: "Welcome to the Rental Car Robot! How can I assist you today?"
    - Delete all other entries under "Agent dialogue"
    - Click "Save" and then click "Test Agent"
    - Enter "Hello"; you should be presented with the appropriate welcome message
    - Close the "Simulator"
* Click "Manage" | "Intents" | "+ Create"
* Use a meaningful name for the intent - e.g., "main.car_rental"
* Under training phrases, enter each of the following:
    - I want to rent a car.
    - Can I book a car for next weekend?
    - I need a rental car.
    - I want to reserve a car.
    - I need a car for the weekend, can you help me?
    - Can I rent a vehicle for my road trip?
    - I’m looking for a car rental service near me.
    - I want to book a luxury car for a special occasion.
    - Can you reserve a car for me next Friday?
    - I need a car for business travel, what do you have?
    - Is it possible to rent an SUV for a family trip?
    - I’d like to hire a car for a few days.
    - What’s the process for booking a rental car?
    - Can I get a convertible for my vacation?
    - I need a rental car with unlimited mileage.
    - Do you have electric cars available for rent?
    - I'd like to rent a car in Columbus for dropoff in Hilton Head
* Notice annotations applied automatically by DialogFlow
* Click "Save"
* Navigate back to "Build" and click on "Start Page"
* Click the + next to "Routes"
* Under "Intent", select your "main.car_rental" intent
* Under "Fulfillment", select "Agent responses", and click "+ Add dialogue response"
* Click "Agent dialogue" and add the following: "Great - I can help you with your car rentail. Let's get some details."
* Under "Transition", select "Page" and "+ new Page" from the dropdown; for "Page name", enter "Get Rental Details"
* Click "Save"
* Click "Test Agent" and enter "Hello"
* Try different variations of an initial request to rent a car to see how the agent reponds; you can reset the conversation in the Simulator by closing it and clicking "Test Agent" again
* Close the Simulator when finished testing
* Click on the "Get Rental Details" page and click the + next to "Parameters"
* Add a parameter for pickup location:
    - For name enter "pickup_location"
    - For "Entity type" use "@sys.geo-city"
    - Ensure that "Required" is checked
    - Under "Initial prompt fulfillment", click "Agent responses" and "+ Add dialogue response"
    - Enter "Where would you like to pick up the car?"
    - Click "Save"
* Add a parameter for rental date:
    - For name enter "rental_date"
    - For "Entity type" use "@sys.date"
    - Ensure that "Required" is checked
    - Under "Initial prompt fulfillment", click "Agent responses" and "+ Add dialogue response"
    - Enter "Great! When do you need the car?"
    - Click "Save"
* Add a parameter for type of car:
    - For name enter "car_type"
    - For "Entity type" use "@sys.any"
    - Ensure that "Required" is checked
    - Under "Initial prompt fulfillment", click "Agent responses" and "+ Add dialogue response"
    - Enter "What type of car would you like to rent (e.g., sedan, SUV, convertible)?"
    - Click "Save"
* Add a parameter for return date:
    - For name enter "return_date"
    - For "Entity type" use "@sys.date"
    - Ensure that "Required" is checked
    - Under "Initial prompt fulfillment", click "Agent responses" and "+ Add dialogue response"
    - Enter "When will you be returning the rental?"
    - Click "Save"
* Within the "Get Rental Details" page, click the + next to "Routes"
* Under "Condition", make sure "Match AT LEAST ONE rule (OR)" is selected
* In the "Parameter" area under "Condition":
    - Enter "$page.params.status" for the parameter name
    - Select "=" from the Operand
    - For Value, enter "FINAL" (including the double quotes)
* Under "Fulfillment", click "Agent responses" and "+ Add dialogue response"
* Enter "Thank you for providing your information. Let me check on the availability of rentals that match your request."
* Scroll down to the bottom under "Transition" and select "Page"
* Select "+ new Page" from the dropdown and enter "Confirm Details" for the page name
* Click "Save"
* Click on the "Confirm Details" page and click "Edit Fulfillment" under "Entry fulfillment"
* Under "Agent responses", click "+ Add dialogue response" and enter the following for the response:

This is to confirm that you would like to rent car type $session.params.car_type to be picked up on $session.params.rental_date in $session.params.pickup_location, and you will be returning the car on $session.params.return_date. Do I have all of that correct?

* Click "Save"
* In your "Confirm Details" page, click the + next to "Routes"
* Under "Intent", click "+ new Intent"
    - Enter "confirmed.yes" for name
    - For training phrases, enter several variations of "yes" (e.g., yes, yep, you got it, etc.)
    - Click "Save"
* Under "Fulfillment", click "Agent responses", and "+ Add dialogue response"
* Enter "Awesome-sauce! You are all set with a rental!"
* Add a new route
* Under "Intent", click "+ new Intent"
    - Enter "confirmed.no" for name
    - For training phrases, enter several variations of "no" (e.g., no, not correct, incorrect, etc.)
    - Click "Save"
* From the "Route" definition section, scroll down to "Transition", click "Page", and choose "Get Rental Details" for the page
* Scroll up to "Parameter presets" and add the following parameters:
    - pickup_location (for value, use null)
    - rental_date (for value, use null)
    - car_type (for value, use null)
    - return_date (for value, use null)
    - This will reset the invalid parameter values for reentry by the user
* You can optionally add an agent response associated to the "no" route (e.g., something like "I'm sorry - let's try that again...")
* Click "Save"
* Click "Test Agent" and try out different variations of interaction with the agent
* Try the "yes" and the "no" path
* If you have time left over, try experimenting with adding additional steps or modifying the configuration of your agent