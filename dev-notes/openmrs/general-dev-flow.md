# 🐎 General Dev Flow

### Steps

**1. Set Up Your Development Environment**

1. **Prerequisites**:
   * Install Java Development Kit (JDK)
   * Install Apache Maven
   * Install MySQL
   * Install Node.js and npm
   * Install Git
2. **Clone OpenMRS Repositories**:
   *   Clone the `openmrs-core` repository:

       ```sh
       shCopy codegit clone https://github.com/openmrs/openmrs-core.git
       cd openmrs-core
       ```
   *   Clone the `openmrs-module-legacyui` repository for the legacy UI:

       ```sh
       shCopy codegit clone https://github.com/openmrs/openmrs-module-legacyui.git
       cd openmrs-module-legacyui
       ```

**2. Backend Customization**

1. **Set Up OpenMRS Core**:
   *   Build and install OpenMRS Core:

       ```sh
       shCopy codemvn clean install
       ```
   * Deploy OpenMRS Core on Apache Tomcat.
2. **Create Custom Modules**:
   *   Create a new module using the OpenMRS SDK:

       ```sh
       shCopy codemvn openmrs-sdk:create-project
       ```
   *   Develop custom logic within your module:

       ```java
       javaCopy codepublic class CustomService {
           public void customMethod() {
               // Custom business logic
           }
       }
       ```
3. **Integrate with External Services (e.g., ML Models)**:
   * Expose your ML models as RESTful services (e.g., using Flask or Django).
   *   Call these services from your OpenMRS module:

       ```java
       javaCopy codeRestTemplate restTemplate = new RestTemplate();
       String result = restTemplate.getForObject("http://ml-service-url/predict", String.class);
       ```

**3. Database Customization**

1. **Schema Management**:
   *   Use Liquibase for database schema changes:

       ```xml
       xmlCopy code<changeSet id="001" author="dev">
           <createTable tableName="custom_table">
               <column name="id" type="int" autoIncrement="true">
                   <constraints primaryKey="true"/>
               </column>
               <column name="name" type="varchar(255)"/>
           </createTable>
       </changeSet>
       ```
   *   Apply changes:

       ```sh
       shCopy codemvn openmrs-sdk:run
       ```

**4. Frontend Customization with O3 (Microfrontends)**

1. **Set Up O3 Frontend**:
   *   Clone the `openmrs-esm-core` repository:

       ```sh
       shCopy codegit clone https://github.com/openmrs/openmrs-esm-core.git
       cd openmrs-esm-core
       ```
   *   Install dependencies:

       ```sh
       shCopy codenpm install
       ```
2. **Create Custom Microfrontend Module**:
   *   Use the OpenMRS Microfrontend CLI to scaffold a new module:

       ```sh
       shCopy codenpm install -g @openmrs/openmrs-esm-cli
       openmrs-esm create custom-module
       cd custom-module
       ```
3. **Develop Your Custom Module**:
   *   Example of a React component:

       ```jsx
       jsxCopy codeimport React from 'react';

       const CustomComponent = () => {
         return (
           <div>
             <h1>Custom Feature</h1>
           </div>
         );
       };

       export default CustomComponent;
       ```
4. **Integrate with Backend**:
   *   Fetch data using the OpenMRS REST API:

       ```js
       jsCopy codeimport axios from 'axios';

       const fetchData = async () => {
         try {
           const response = await axios.get('/openmrs/ws/rest/v1/patient');
           console.log(response.data);
         } catch (error) {
           console.error('Error fetching data', error);
         }
       };

       fetchData();
       ```
5. **Register and Configure Module**:
   * Register your custom module in the `openmrs-esm-core` configuration.

**5. Testing and Deployment**

1. **Unit and Integration Testing**:
   * Write tests for your backend services and frontend components.
   * Use JUnit for backend testing and Jest for frontend testing.
2. **Build and Deploy**:
   *   Build your backend and frontend:

       ```sh
       shCopy codemvn clean package
       npm run build
       ```
   * Deploy to your desired environment (e.g., AWS, Azure).
3. **Continuous Integration and Deployment (CI/CD)**:
   * Set up CI/CD pipelines using tools like Jenkins, GitHub Actions, or Travis CI to automate testing and deployment.

#### Example Project Structure

Here's an example structure of your project components:

```bash
bashCopy code/my-custom-ehr
    /backend
        /openmrs-core
        /openmrs-module-custom
    /frontend
        /openmrs-esm-core
        /custom-module
    /db
        /liquibase-changesets
    /ml-services
        /predictive-model
        /summarization-model
```
