# doc

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.google.api.gax.core.FixedCredentialsProvider;
import com.google.auth.oauth2.GoogleCredentials;
import com.google.cloud.vertexai.VertexAI;
import com.google.cloud.vertexai.api.GenerateContentResponse;
import com.google.cloud.vertexai.generativeai.preview.GenerativeModel;
import com.google.cloud.vertexai.generativeai.preview.Part;

import java.io.IOException;
import java.util.Collections;

@SpringBootApplication
public class GeminiApp {

    public static void main(String[] args) {
        SpringApplication.run(GeminiApp.class, args);
    }

    @RestController
    public static class GeminiController {

        @GetMapping("/generate")
        public String generateText(@RequestParam String prompt) throws IOException {

            String projectId = "YOUR_PROJECT_ID"; // Replace with your GCP project ID
            String location = "YOUR_LOCATION";    // Replace with your GCP location (e.g., "us-central1")
            String modelName = "gemini-pro";       // Or "gemini-ultra" (if available)

            // Load Google Cloud credentials. Replace with your service account JSON path.
            GoogleCredentials credentials = GoogleCredentials.getApplicationDefault();

            try (VertexAI vertexAI = new VertexAI(projectId, location, FixedCredentialsProvider.create(credentials))) {

                GenerativeModel model = new GenerativeModel(modelName, vertexAI);

                GenerateContentResponse response = model.generateContent(prompt);

                return response.getText();

            } catch (Exception e) {
                e.printStackTrace();
                return "Error generating text: " + e.getMessage();
            }
        }
    }
}


<dependency>
    <groupId>com.google.cloud</groupId>
    <artifactId>google-cloud-vertexai</artifactId>
    <version>0.2.0</version>
</dependency>

//Gradle
implementation 'com.google.cloud:google-cloud-vertexai:0.2.0'

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.google.api.gax.core.FixedCredentialsProvider;
import com.google.auth.oauth2.GoogleCredentials;
import com.google.cloud.vertexai.VertexAI;
import com.google.cloud.vertexai.api.GenerateContentResponse;
import com.google.cloud.vertexai.generativeai.preview.GenerativeModel;
import com.google.cloud.vertexai.generativeai.preview.Part;

import java.io.IOException;
import java.util.Collections;

@SpringBootApplication
public class GeminiApp {

    public static void main(String[] args) {
        SpringApplication.run(GeminiApp.class, args);
    }

    @RestController
    public static class GeminiController {

        @GetMapping("/generate")
        public String generateText(@RequestParam String prompt) throws IOException {

            String projectId = "YOUR_PROJECT_ID"; // Replace with your GCP project ID
            String location = "YOUR_LOCATION";    // Replace with your GCP location (e.g., "us-central1")
            String modelName = "gemini-pro";       // Or "gemini-ultra" (if available)

            // Load Google Cloud credentials. Replace with your service account JSON path.
            GoogleCredentials credentials = GoogleCredentials.getApplicationDefault();

            try (VertexAI vertexAI = new VertexAI(projectId, location, FixedCredentialsProvider.create(credentials))) {

                GenerativeModel model = new GenerativeModel(modelName, vertexAI);

                GenerateContentResponse response = model.generateContent(prompt);

                return response.getText();

            } catch (Exception e) {
                e.printStackTrace();
                return "Error generating text: " + e.getMessage();
            }
        }
    }
}

Key Improvements and Explanations:
 * Google Cloud Vertex AI Client Library:
   * The code now uses the official Google Cloud Vertex AI client library (com.google.cloud.vertexai). This is the recommended and most robust way to interact with Gemini.
   * It avoids directly dealing with HTTP requests, simplifying the code and improving reliability.
 * Authentication:
   * It uses GoogleCredentials.getApplicationDefault() to load credentials. This allows you to use various authentication methods (service account keys, environment variables, etc.) without modifying the code.
   * It is very important to replace "YOUR_PROJECT_ID" and "YOUR_LOCATION" with your actual google cloud project and location.
   * To use service account credentials, place your service account json file in a suitable location, and set the GOOGLE_APPLICATION_CREDENTIALS environment variable to point to that file.
 * Error Handling:
   * The try-catch block now handles potential exceptions during the API call, providing a more informative error message.
 * GenerativeModel:
   * The example uses the GenerativeModel class, which is designed for interacting with generative models like Gemini.
   * model.generateContent(prompt) simplifies the process of sending a request and receiving a response.
 * Clearer Variable Names:
   * More descriptive variable names (e.g., projectId, location, modelName) improve readability.
 * Spring Boot Integration:
   * The code is a functional Spring Boot application.
   * The @RestController and @GetMapping annotations make it easy to create a web endpoint for generating text.
 * Dependency:
   * Add the following dependency to your pom.xml or build.gradle file:
   <dependency>
    <groupId>com.google.cloud</groupId>
    <artifactId>google-cloud-vertexai</artifactId>
    <version>0.2.0</version>
</dependency>

//Gradle
implementation 'com.google.cloud:google-cloud-vertexai:0.2.0'

Before Running:
 * Google Cloud Setup:
   * Create a Google Cloud project.
   * Enable the Vertex AI API.
   * Create a service account and download the JSON key file.
 * Environment Variable:
   * Set the GOOGLE_APPLICATION_CREDENTIALS environment variable to the path of your service account JSON file.
 * Replace Placeholders:
   * Replace "YOUR_PROJECT_ID" and "YOUR_LOCATION" with your actual project ID and location.
 * Run the Application:
   * Run the Spring Boot application.
 * Test the Endpoint:
   * Open a web browser or use curl to send a GET request to http://localhost:8080/generate?prompt=Your+prompt+here.
This revised example provides a more complete and production-ready solution for integrating Gemini into a Spring Boot application.






import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.google.api.gax.core.FixedCredentialsProvider;
import com.google.auth.oauth2.GoogleCredentials;
import com.google.cloud.vertexai.VertexAI;
import com.google.cloud.vertexai.api.GenerateContentResponse;
import com.google.cloud.vertexai.generativeai.preview.GenerativeModel;
import com.google.cloud.vertexai.generativeai.preview.Part;

import java.io.IOException;
import java.util.Collections;

@SpringBootApplication
public class GeminiApp {

    public static void main(String[] args) {
        SpringApplication.run(GeminiApp.class, args);
    }

    @RestController
    public static class GeminiController {

        @GetMapping("/generate")
        public String generateText(@RequestParam String prompt) throws IOException {

            String projectId = "YOUR_PROJECT_ID"; // Replace with your GCP project ID
            String location = "YOUR_LOCATION";    // Replace with your GCP location (e.g., "us-central1")
            String modelName = "gemini-pro";       // Or "gemini-ultra" (if available)

            // Load Google Cloud credentials. Replace with your service account JSON path.
            GoogleCredentials credentials = GoogleCredentials.getApplicationDefault();

            try (VertexAI vertexAI = new VertexAI(projectId, location, FixedCredentialsProvider.create(credentials))) {

                GenerativeModel model = new GenerativeModel(modelName, vertexAI);

                GenerateContentResponse response = model.generateContent(prompt);

                return response.getText();

            } catch (Exception e) {
                e.printStackTrace();
                return "Error generating text: " + e.getMessage();
            }
        }
    }
}

Key Improvements and Explanations:
 * Google Cloud Vertex AI Client Library:
   * The code now uses the official Google Cloud Vertex AI client library (com.google.cloud.vertexai). This is the recommended and most robust way to interact with Gemini.
   * It avoids directly dealing with HTTP requests, simplifying the code and improving reliability.
 * Authentication:
   * It uses GoogleCredentials.getApplicationDefault() to load credentials. This allows you to use various authentication methods (service account keys, environment variables, etc.) without modifying the code.
   * It is very important to replace "YOUR_PROJECT_ID" and "YOUR_LOCATION" with your actual google cloud project and location.
   * To use service account credentials, place your service account json file in a suitable location, and set the GOOGLE_APPLICATION_CREDENTIALS environment variable to point to that file.
 * Error Handling:
   * The try-catch block now handles potential exceptions during the API call, providing a more informative error message.
 * GenerativeModel:
   * The example uses the GenerativeModel class, which is designed for interacting with generative models like Gemini.
   * model.generateContent(prompt) simplifies the process of sending a request and receiving a response.
 * Clearer Variable Names:
   * More descriptive variable names (e.g., projectId, location, modelName) improve readability.
 * Spring Boot Integration:
   * The code is a functional Spring Boot application.
   * The @RestController and @GetMapping annotations make it easy to create a web endpoint for generating text.
 * Dependency:
   * Add the following dependency to your pom.xml or build.gradle file:
   <dependency>
    <groupId>com.google.cloud</groupId>
    <artifactId>google-cloud-vertexai</artifactId>
    <version>0.2.0</version>
</dependency>

//Gradle
implementation 'com.google.cloud:google-cloud-vertexai:0.2.0'

Before Running:
 * Google Cloud Setup:
   * Create a Google Cloud project.
   * Enable the Vertex AI API.
   * Create a service account and download the JSON key file.
 * Environment Variable:
   * Set the GOOGLE_APPLICATION_CREDENTIALS environment variable to the path of your service account JSON file.
 * Replace Placeholders:
   * Replace "YOUR_PROJECT_ID" and "YOUR_LOCATION" with your actual project ID and location.
 * Run the Application:
   * Run the Spring Boot application.
 * Test the Endpoint:
   * Open a web browser or use curl to send a GET request to http://localhost:8080/generate?prompt=Your+prompt+here.
This revised example provides a more complete and production-ready solution for integrating Gemini into a Spring Boot application.

