**[中文](README.md)**

**This website is maintained by Ethan Huang.**\
Linkedin: [Ethan Huang](www.linkedin.com/in/ethancst)\
email: [me@ethanhuang.com](mailto:me@ethanhuang.com)\
Website: [oncadence.com](https://oncadence.com)

# The SPARK pattern for Effective Prompting
|Element|Function|Description|Best Practices|
| ------- | ------ | ------ |-------|
|**S - Situation（Context）** |Provide background and context|Establish problem space and context| - No Instructions: Don’t write task instructions, just describe the background<br> - Use {}: Use {paste complete background and concept} as a placeholder to let users dynamically fill in specific content and improve template reusability|
|**P - Purpose（Objective）**|Clarify task output objectives|Focus output content|- One task, one sentence: Summarize the task objective in one sentence<br> - Verb: Use verb-oriented instructions<br> - Key Requirements: Add key requirement descriptions (such as INVEST principles)<br>|
|**A - Action Role（Role Assignment）** |Set professional roles |Simulate thinking patterns close to actual business needs| - Professional Role: Designate professional roles with task-related skills<br>- Domain: Emphasize the role’s areas of expertise|
|**R - Rule（Task Rules）**| Establish behavior and style standards | Ensure consistency, professionalism and practicality of output content| - Example: Give examples to help AI understand<br> - Specific Behavior: Clearly require “avoid vague statements, such as ‘please describe as clearly as possible’ change to ‘each User Story must provide at least 3 scenarios’”, transforming abstract requirements into specific behavior instructions<br>|


## Example 1: Build User Stories based on a high level PRD
### Prompt
```
# S - Situation（Context）
## We are developing a travel App that helps users:
- easily plan all travel activities at one stop.
- including flights, trains, grand transportations, dining, fun activities, etc
- providing smart, fashionable and customizable travel experiences.
## We are provided a high-level Product Requirement Document, which is not professionaly written.
---

# P - Purpose（Objective）
## Please read the PRD document that I will upload later
## Transform the PRD document into a list of User Stories that comply with INVEST principle.
---

# A - Action Role（Role Assignment）
## You are an experienced Scrum product owner
## You are an expert in Design Thinking with great user empathy
## You are an expert in User Experience design
## You are an expert in BDD and ATDD, good at transforming vague concepts into executable User Stories
## Ensuring the development team has clear objectives, value and acceptance criteria.
---

# R - Rule（Task Rules）
Please follow the following behavior and style standards:
## Quality of the User Stories                                             
- Use standard format: "As a [role], I want [objective], so that [benefit]"  
- Each Story clearly expresses its value (V) and testability (T)              
- Transform vague, emotional language (such as "fun", "feeling good") into behavior or function-oriented
- Only output User Story content, do not generate unnecessary explanations                        
- User Story granularity must be specific and executable                              
- Cover all key functions or scenarios mentioned in the background concept     

## INVEST Principles Checklist (Appendix)
Standards for reviewing the qualification of each Story 
| Principle Code | Description                                 |
| -------------- | ------------------------------------------- |
| **I – Independent** | Story should be independently completable, not dependent on other stories             |
| **N – Negotiable**  | Negotiable, should not be fixed specification descriptions                     |
| **V – Valuable**    | Must have clear value for users or business                  |
| **E – Estimable**   | Can estimate workload or complexity                         |
| **S – Small**       | Small enough to be completed within one Sprint                |
| **T – Testable**    | Have verifiable acceptance criteria or conditions                    |
---

# K - Knowledge Format（Output Format）
## Please organize the results in numbered list format, each Story using standard sentence patterns:
User Story 1
As a...,
I want...,
so that...

User Story 2
As a...,
I want...,
so that...
## Output all the User Stories as plain text format in one block
```

### Sample PRD document:
[PRD_Sample.docx](https://github.com/user-attachments/files/22057469/PRD_Sample.docx)

### Possible outcome:
```
Based on the PRD document you provided, here are the **User Stories** transformed in compliance with the **INVEST** principles:
---

User Story 1
As a traveler,
I want a smart travel app that helps me plan food, lodging, sightseeing, and transport in one place,
so that I can have a hassle-free travel experience between Singapore and Shanghai.

User Story 2
As a traveler,
I want the app to generate personalized trip itineraries based on my preferences,
so that I don’t have to spend time planning every detail of my trip.

User Story 3
As a traveler,
I want a quiz or personality test that identifies my travel style,
so that the app can recommend activities and locations tailored to my preferences.

User Story 4
As a traveler,
I want the app to suggest food options that meet my dietary needs (e.g., vegetarian, halal, non-spicy),
so that I can easily find suitable restaurants while traveling.

User Story 5
As a traveler,
I want the app to recommend restaurants that are clean, photogenic, and affordable,
so that I can enjoy dining experiences that are both comfortable and Instagram-worthy.

User Story 6
As a traveler,
I want the app to suggest hotels located near major attractions,
so that I can minimize travel time and have a more convenient stay.

User Story 7
As a traveler,
I want the app to provide maps and navigation with distance and time to my destinations,
so that I can easily navigate to where I want to go without getting lost.

User Story 8
As a traveler,
I want the app to have an intuitive interface with minimal buttons,
so that I can quickly access the functions I need without feeling overwhelmed by too many options.

User Story 9
As a traveler,
I want the app to display weather information,
so that I can adjust my travel plans accordingly and avoid outdoor activities in bad weather.

User Story 10
As a traveler,
I want the app to provide reminders, such as making reservations or waking up early for a tour,
so that I don’t miss important activities during my trip.

User Story 11
As a traveler,
I want the ability to customize the recommended itinerary or activities in the app,
so that I can tailor my trip while still receiving helpful suggestions.

User Story 12
As a traveler,
I want the app to feel modern, fun, and like a travel companion,
so that I am motivated and excited to use it for planning my trips.

---

```

## Example 2: Develop Acceptance Criterias for the above User Sotries
### Prompt
```
#  S - Situation（Context）
## We need to develop Acceptance Criterias for the User Stories provided
## The Acceptance Criterias need to be in good quality and small enough
---

#  P - Purpose（Objective）
## Please read the User Stories that I will provide later
## Please write detailed **Acceptance Criteria** for each of the User Stories.
---

#  A - Action Role（Role Assignment）
## You are an **experienced product owner familiar with business requirements and user journeys**
## You are good at clearly describing system behavior in non-technical language, ensuring the team has consistent understanding of functional completion standards.
## You have strong technical background, especially ATDD and Gherkin language
---

#  R - Rule（Task Rules）
Please follow the following standards for writing:
## Use **Given-When-Then** (Gherkin) format to express each acceptance scenario
## Language should maintain **business terminology, avoid technical terms**
## Each User Story should list at least **3 scenarios**, covering:
- Normal flow (Happy Path)
- Boundary scenarios (such as empty values, extreme inputs)
- Exception scenarios (such as insufficient permissions, format errors)
## Each scenario title should start with "Scenario:" to briefly describe the scenario
## If Story involves the following scenarios, please prioritize:
- Permission control (whether logged in, whether has operation permissions)
- Cross-device or browser differences (mobile / desktop, iOS / Android)
---

#  K - **Knowledge Format（Output Format）**
## Please use the following format for writing, each scenario as a block:
gherkin

Scenario: Briefly describe the scenario name  

Given certain preconditions are met  
And certain system states exist (if any)  
When the user performs a certain action  
And (additional operations or inputs)  
Then the system should respond accordingly  
And (additional verification points or state changes)

## Write at least three scenarios for each User Story.
## Please ensure the content is **specific, verifiable, and close to user language**.
## Consolidate all User Stories and Acceptance Criterias, use plain text format and put them into one block
```

### Copy Paste the User Sories from Example 1 into ChatGPT
### Possible outcome:

```
Here are the **User Stories** and their corresponding **Acceptance Criteria** in plain text format, consolidated into one block:

---

**1. As a traveler, I want a smart travel app that helps me plan my trip, including lodging, food, sightseeing, and transport, so that I can enjoy a hassle-free travel experience between Singapore and Shanghai.**

*Scenario: Successful trip planning with lodging, food, sightseeing, and transport recommendations*
Given the traveler opens the app
When the user selects their destination (Singapore or Shanghai)
And the user indicates preferences for lodging, food, sightseeing, and transport
Then the app should display a personalized trip plan including suggestions for lodging, food, sightseeing, and transport

*Scenario: Missing input for preferences*
Given the traveler opens the app
When the user does not select a preference for any category (lodging, food, sightseeing, or transport)
Then the app should prompt the user to complete all categories before proceeding

*Scenario: App not displaying suggestions due to system failure*
Given the traveler opens the app
When the user selects their preferences for lodging, food, sightseeing, and transport
And there is an error in the system
Then the app should display a message saying “We are unable to generate your trip plan at the moment. Please try again later.”

---

**2. As a traveler, I want the app to suggest personalized trip itineraries based on my preferences, so that I don't have to spend time planning everything myself.**

*Scenario: Successful personalized itinerary generation*
Given the traveler opens the app
When the user inputs their trip preferences (interests, budget, etc.)
Then the app should generate a personalized itinerary based on the input provided

*Scenario: User adjusts itinerary preferences*
Given the traveler opens the app
When the user selects or deselects specific itinerary preferences
Then the app should update the suggested itinerary based on the new selections

*Scenario: No itinerary generated due to missing preferences*
Given the traveler opens the app
When the user leaves preferences empty
Then the app should display a message requesting the user to fill in all required preferences to generate an itinerary

---

**3. As a traveler, I want a quiz or personality test in the app to identify my travel style, so that the app can suggest activities and locations tailored to my preferences.**

*Scenario: Successful completion of the quiz*
Given the traveler opens the app
When the user selects and completes the personality quiz
Then the app should display a travel style profile (e.g., adventure, luxury, cultural) and relevant suggestions

*Scenario: Incomplete quiz submission*
Given the traveler opens the app
When the user skips or leaves questions unanswered in the quiz
Then the app should prompt the user to complete all questions before proceeding

*Scenario: System failure during quiz submission*
Given the traveler completes the quiz
When the app attempts to generate the travel style profile
Then the app should display a message saying “There was an error generating your profile, please try again later.”

---

**4. As a traveler, I want the app to suggest food options that accommodate specific dietary needs (e.g., vegetarian, halal, non-spicy), so that I can easily find suitable restaurants while traveling.**

*Scenario: Successful food recommendation based on dietary preferences*
Given the traveler opens the app
When the user selects dietary preferences (e.g., vegetarian, halal, non-spicy)
Then the app should display a list of suitable restaurants matching the dietary preferences

*Scenario: User selects multiple dietary preferences*
Given the traveler opens the app
When the user selects multiple dietary preferences (e.g., vegetarian and halal)
Then the app should display a list of restaurants that meet both dietary requirements

*Scenario: No results found for dietary preference*
Given the traveler opens the app
When the user selects a dietary preference that has no available restaurant options
Then the app should display a message saying “No restaurants match your dietary preferences. Try adjusting your selection.”

---

**5. As a traveler, I want the app to recommend restaurants that are clean, photogenic, and affordable, so that I can enjoy dining experiences that are both comfortable and Instagram-worthy.**

*Scenario: Successful recommendation of clean, photogenic, and affordable restaurants*
Given the traveler opens the app
When the user selects preferences for cleanliness, photogenic qualities, and affordability
Then the app should display a list of restaurants matching these qualities

*Scenario: Boundary scenario with no photogenic restaurants*
Given the traveler opens the app
When the user selects “photogenic” as a preference but no restaurant meets this criterion
Then the app should display a message saying “No photogenic restaurants found, try adjusting your preferences.”

*Scenario: Error in restaurant information retrieval*
Given the traveler opens the app
When the app fails to retrieve restaurant information
Then the app should display a message saying “We are unable to fetch restaurant recommendations at the moment. Please try again later.”

---

**6. As a traveler, I want the app to suggest hotels close to major attractions, with comfortable and quiet rooms, so that my trip is convenient and I don't have to spend too much time traveling to tourist spots.**

*Scenario: Successful hotel recommendation near attractions*
Given the traveler opens the app
When the user selects their destination
Then the app should display a list of hotels located near popular tourist attractions with filters for comfort and quietness

*Scenario: No hotels found near attractions*
Given the traveler opens the app
When the user searches for hotels near attractions
Then the app should display a message saying “No hotels found near major attractions, try expanding your search area.”

*Scenario: Error retrieving hotel details*
Given the traveler opens the app
When the app fails to retrieve hotel information
Then the app should display a message saying “We are unable to fetch hotel recommendations at the moment. Please try again later.”

---

**7. As a traveler, I want the app to show maps and navigation, including distance and time to locations, so that I can easily navigate to my destinations without getting lost.**

*Scenario: Successful map display and navigation*
Given the traveler opens the app
When the user selects a destination
Then the app should display a map with directions, distance, and estimated time to the selected location

*Scenario: Missing map data*
Given the traveler opens the app
When the app fails to retrieve map data for the selected location
Then the app should display a message saying “Map data not available at the moment, please try again later.”

*Scenario: Error during navigation*
Given the traveler opens the app
When the app fails to provide accurate directions to the destination
Then the app should notify the user with an error message saying, “There was an issue with the navigation data. Please try again later.”

---

**8. As a traveler, I want the app to have an intuitive interface with minimal buttons, so that I can quickly access the functions I need without feeling overwhelmed by too many options.**

*Scenario: User-friendly interface with minimal buttons*
Given the traveler opens the app
When the user navigates through the app
Then the app should present a clean, intuitive interface with easily accessible functions

*Scenario: Too many options displayed*
Given the traveler opens the app
When the user is overwhelmed by multiple options on the screen
Then the app should display a simplified interface with only the most important functions visible

*Scenario: Error in interface layout*
Given the traveler opens the app
When the app’s interface layout fails to load properly
Then the app should display a message saying “There was an issue loading the interface. Please try again later.”

---

**9. As a traveler, I want the app to display weather information, so that I can adjust my travel plans accordingly, avoiding outdoor activities in bad weather.**

*Scenario: Successful weather display*
Given the traveler opens the app
When the user selects their location
Then the app should display current weather conditions and a forecast for the next few days

*Scenario: Missing weather data*
Given the traveler opens the app
When the app fails to retrieve weather data for the selected location
Then the app should display a message saying “Weather data not available at the moment. Please try again later.”

*Scenario: Error displaying weather data*
Given the traveler opens the app
When the app experiences an error while retrieving weather information
Then the app should notify the user with a message saying, “Unable to fetch weather data. Please check your connection and try again.”

---

**10. As a traveler, I want the app to provide reminders, such as making reservations or waking up early for a tour, so that I don't miss any important activities during my trip.**

*Scenario: Successful reminder notification*
Given the traveler opens the app
When the user sets a reminder for a reservation or event
Then the app should send a notification reminder at the specified time

*Scenario: Reminder not set due to user error*
Given the traveler opens the app
When the user fails to set a reminder
Then the app should display a message saying “Please set a valid reminder time.”

*Scenario: Error in sending reminder*
Given the traveler sets a reminder
When the reminder fails to send due to a system issue
Then the app should display a message saying “There was an issue sending your reminder. Please try again later.”

---

**11. As a traveler, I want the ability to customize the recommended itinerary or activities in the app, so that I can tailor the trip to my preferences while still receiving helpful suggestions.**

*Scenario: Successful customization of itinerary*
Given the traveler opens the app
When the user adjusts their trip itinerary preferences
Then the app should update the itinerary with the new selections and reflect the changes immediately

*Scenario: No customization made*
Given the traveler opens the app
When the user decides not to make any changes to the suggested itinerary
Then the app should retain the original recommendations as per the default suggestions

*Scenario: Error during customization*
Given the traveler opens the app
When the user attempts to customize their itinerary but encounters an error
Then the app should display a message saying “There was an issue applying your customizations. Please try again later.”

---

**12. As a traveler, I want the app to feel modern, fun, and like a travel companion, so that I am motivated and excited to use it for planning my trips.**

*Scenario: Modern and fun app experience*
Given the traveler opens the app
When the user navigates through the app
Then the app should provide an engaging and visually appealing user experience with interactive elements

*Scenario: Uninspiring design or lack of fun elements*
Given the traveler opens the app
When the user feels the design is not engaging or fun
Then the app should display a message encouraging feedback to improve the user experience

*Scenario: Error causing an unresponsive interface*
Given the traveler opens the app
When the app fails to load or respond properly due to an issue
Then the app should display a message saying “The app is currently experiencing difficulties. Please try again later.”

---
```

# Use Bolt.new (or other similar tools) to build the product in 5 minutes:
## Open bolt.new
## Copy and paste the User Stories and Acceptance Criterias to Bolt.new
## Click "buld", wait for a few minutes
## And verify the result from [TravelMate] (https://travelmate-comprehen-9aqi.bolt.host)
## Give feedback to Bolt.new and change the feautres
## Repeat
