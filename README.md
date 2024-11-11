# Human Subject Experiment Infrastructure for AI Fairness Studies

This repository provides infrastructure for conducting human subject experiments to explore participants' engagement, strategic responses, and fairness perceptions in interactions with AI-based decision systems. Over the years, three extensive versions of this web app have been developed to support various research directions, with the latest and most robust version now publicly available. These experiments support research on how fairness perceptions evolve in the presence of qualification improvement opportunities and over repeated interactions with AI systems, as studied in the following research:

- **Understanding Decision Subjects' Engagement with and Perceived Fairness of AI Models When Opportunities of Qualification Improvement Exist**  
  *Authors*: Meric Altug Gemalmaz and Ming Yin  
  *Abstract*: This study investigates how the fairness of an AI model’s decisions impacts people’s engagement with the model and their fairness perceptions when they can strategically respond. We consider two forms of strategic response: choosing whether to continue interacting with the model and deciding whether to invest in self-improvement to enhance future favorable outcomes. Across three human-subject experiments, findings reveal that decision subjects' willingness to engage or improve does not vary with the model's fairness, even when it displays bias against certain protected attributes. However, subjects perceive the model as less fair when it systematically discriminates against their group, particularly when qualification improvements are more challenging for less qualified individuals.

- **Understanding Decision Subjects' Fairness Perceptions and Retention in Repeated Interactions with AI-Based Decision Systems**  
  *Authors*: Meric Altug Gemalmaz and Ming Yin  
  *Conference*: 5th AAAI/ACM Conference on AI, Ethics, and Society (AIES), Oxford, UK, August 2022  
  *Abstract*: In this paper, we examine fairness perceptions and retention in repeated interactions with an AI-based decision system. By studying an AI-driven loan lending system, we analyze how fairness perceptions and retention are influenced when decision subjects can repeatedly engage and respond to the system. The findings suggest that subjects' perceptions and engagement are more influenced by whether the system favors their group than by unbiased treatment across groups. Additionally, subjects with varying qualification levels respond differently to both biased group treatment and system tendencies to favor or disfavor their own group. While retention is primarily driven by subjects' personal prospects for favorable outcomes, their fairness perceptions are shaped by how the system treats individuals in other groups in a nuanced way.

### Overview
This project offers a structured environment for controlled experiments with human participants, focusing on interactions and fairness perceptions within AI-based decision systems. It provides setup instructions, usage guides, and materials necessary to replicate the experimental setup for further research and validation.

### Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/mgemalma/Human-subject-experiment-infrastructure.git
    cd Human-subject-experiment-infrastructure
    ```

2. **Install dependencies**:
    Ensure you have [Node.js](https://nodejs.org/) and [Meteor](https://www.meteor.com/) installed. Then run:
    ```bash
    npm install
    ```

### Usage

#### Starting the Application
- **Run the Meteor App**:
    ```bash
    meteor
    ```
    This command starts the Meteor server for local development.

#### Monitoring Database Changes
To observe real-time changes in the MongoDB collections, open a separate terminal and run:
```bash
meteor mongo
```
#### Running the Web App

To run the web app, use a URL structured as follows:

```plaintext
http://localhost:3000/?workerId=<worker_id>&assignmentId=<assignment_id>&hitId=<hit_id>&turkSubmitTo=<submission_url>
```
## Deployment

To deploy the Meteor app locally, use the following example commands to set up the environment variables and start the application:

```bash
# Set the port number for the application
port_num='127.0.0.1:3000'

# Set the root URL for the application
root_url='https://yourdomain.com/yourapp'

# Export the ROOT_URL and BIND_UP variables
export ROOT_URL=$root_url
export BIND_UP=$port_num

# Start the Meteor app on the specified port
meteor run --port $port_num

# Notify deployment completion
echo "Deployment finished"
```

### Project Directory Overview

- **client/**: Contains all client-side code for the web application.
  - **client/main.js**: Contains essential code for experiment settings, including imports of HTML and JavaScript files, timing configurations, qualification settings, bonus amounts, conversion rates, credit score thresholds, improvement costs, and other experimental parameters. It also includes functions for managing registration, session handling, and user data verification.
  - **client/main.html**: Provides the head section required for the web app to run, though not actively used by the project.
  - **client/main.css**: Includes styling necessary for the app, though not actively used.
  - **client/mainindex/**: Holds all the HTML files used in each specific view of the web app.
    - **Improvement.html**: A view related to user improvement tracking or feedback.
    - **accept.html**: A view to remind the user of their acceptance of the experiment and agreement to the terms.
    - **consent.html**: A demo consent form for participant agreement, which researchers should modify according to their specific experiment requirements.
    - **error.html**: Contains error messages and respective templates for displaying errors to users.
    - **first.html**: The initial template that loads first; other HTML templates are rendered within this template to create a unified user interface.
    - **home.html**: The initial welcome view displayed to users when they enter the web app.
    - **inst_profile.html**: Allows users to select an avatar and nickname, enhancing the user-friendliness of the interaction.
    - **instr-2.html**: Provides tutorials where users learn about their own persona fields.
    - **instr-3.html**: Presents instructions for the experiment to the users.
    - **qualification.html**: Contains a quiz to assess user understanding of the tutorial content.
    - **refresh.html**: Displays an error message if something goes wrong during the interaction.
    - **survey.html** and **survey1.html**: The first and second pages of the survey interfaces for participant feedback.
    - **taskDesign.html**: The main view where the experiment is conducted.
    - **trns_qual.html**: A transitional view displayed to participants before the experiment begins, notifying them that they passed the quiz.
  - **client/Scripts/**: Contains JavaScript files corresponding to most HTML files, handling specific functionalities for each view.
    - **Home.js**: Manages parts of the navigation by directing users to the appropriate view within the web app when a link is modified.
    - **Improvement.js**: Contains the script for the improvement view.
    - **index_manager.js**: Determines which view the user should navigate to by maintaining a global index count for each user.
    - **inst_profile.js**: Supports the avatar and nickname selection in the user profile setup.
    - **instr-2.js**: Provides the script to explain the assigned user persona to the user.
    - **instr-3.js**: Contains the script for the third instructional view.
    - **intro.min.js**: Includes code for intro.js functionality.
    - **qualification.js**: Contains the code for the qualification quiz.
    - **register.js**: Registers users and creates accounts in the Meteor app for data tracking.
    - **router.js**: Defines additional paths, mainly for error handling.
    - **survey.js** and **survey1.js**: Handle saving and recording survey responses.
    - **task.js**: Powers the main experiment interface, handling interactions for the primary user experience.

- **collections/task-collection.js**: Defines MongoDB collections used in the project, which serve as the structure for storing data in the database:
  - **UserAdv**: Stores all user data.
  - **Fairness**: Contains fairness components of the AI model.
  - **TaskState**: Records everything the user sees in a single interaction with the AI model.
  - **Bonus**: Tracks the bonus earned by each user.
  - **Captcha**: Stores client-side CAPTCHA information shown to the user.
  - **CaptchaPrivate**: Used by the server to verify if the user solved the CAPTCHA correctly.


- **private/**: Contains items accessible only by the server, such as CAPTCHA images used to add an extra security layer on top of Google CAPTCHA. This directory supports server-only access for secure handling of CAPTCHA verification images.

- **public/**: Contains images and other public assets used within the web application interface.

- **server/**: Contains server-side code and functionalities.
  - **server/main.js**: Manages server-side operations, including data insertion into the database and other behind-the-scenes tasks for the web app.



### Dependencies

This project includes a range of dependencies necessary for data handling, visualization, fingerprinting, and interface functionality:
- `@babel/runtime`, `@fingerprintjs/botd`, `@fingerprintjs/fingerprintjs`, `@fingerprintjs/fingerprintjs-pro`, `aws-sdk`, `bcrypt`, `canvas`, `d3`, `d3-sankey`, `driver.js`, `express`, `filereader`, `fingerprintjs2`, `http-proxy`, `intro.js`, `jStat`, `js-base64`, `meteor-node-stubs`, `sweetalert2`

### Configuration

To protect the application from bots, this project uses Google CAPTCHA. You'll need to add your own Google CAPTCHA secret key in the configuration.

1. **Obtain a CAPTCHA Key**:
   - Go to [Google reCAPTCHA](https://www.google.com/recaptcha) and sign up for an API key.

2. **Set Up the CAPTCHA Key**:
   - In `server/main.js`, locate line 168 and replace `'YOUR CAPTCHA SECRET KEY'` with your Google CAPTCHA secret key.

This ensures that CAPTCHA is correctly configured for bot protection during interactions with the application.

### License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

### License (MIT License)

```markdown
MIT License with Attribution Requirement

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

1. **Attribution Requirement**: Users of this software are required to give appropriate credit to the original author, Meric Altug Gemalmaz, in any derivative works, publications, or software distributions that utilize this software. This includes a citation to relevant research papers where applicable.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.