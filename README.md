# Automation-Assessment-Task
### **Files in the Repository:**

1. **LoginPage.java** (Page Object Model class for Login page):
   ```java
   package com.automation.pages;

   import org.openqa.selenium.By;
   import org.openqa.selenium.WebDriver;
   import org.openqa.selenium.WebElement;

   public class LoginPage {

       WebDriver driver;

       // Locators for elements
       By emailField = By.id("email");
       By passwordField = By.id("password");
       By loginButton = By.id("loginButton");
       By errorMessage = By.id("errorMessage");

       // Constructor
       public LoginPage(WebDriver driver) {
           this.driver = driver;
       }

       // Method to enter email
       public void enterEmail(String email) {
           driver.findElement(emailField).sendKeys(email);
       }

       // Method to enter password
       public void enterPassword(String password) {
           driver.findElement(passwordField).sendKeys(password);
       }

       // Method to click on login button
       public void clickLogin() {
           driver.findElement(loginButton).click();
       }

       // Method to get error message
       public String getErrorMessage() {
           return driver.findElement(errorMessage).getText();
       }
   }

2. **SignUpPage.java** (Page Object Model class for Sign-up page):
   ```java
   package com.automation.pages;

   import org.openqa.selenium.By;
   import org.openqa.selenium.WebDriver;

   public class SignUpPage {

       WebDriver driver;

       // Locators for elements
       By nameField = By.id("name");
       By emailField = By.id("email");
       By passwordField = By.id("password");
       By signUpButton = By.id("signUpButton");
       By errorMessage = By.id("errorMessage");

       // Constructor
       public SignUpPage(WebDriver driver) {
           this.driver = driver;
       }

       // Method to enter name
       public void enterName(String name) {
           driver.findElement(nameField).sendKeys(name);
       }

       // Method to enter email
       public void enterEmail(String email) {
           driver.findElement(emailField).sendKeys(email);
       }

       // Method to enter password
       public void enterPassword(String password) {
           driver.findElement(passwordField).sendKeys(password);
       }

       // Method to click on sign-up button
       public void clickSignUp() {
           driver.findElement(signUpButton).click();
       }

       // Method to get error message
       public String getErrorMessage() {
           return driver.findElement(errorMessage).getText();
       }
   }

3. **LoginTest.java** (Test class using JUnit and Selenium):
   ```java
   package com.automation.tests;

   import org.junit.Assert;
   import org.junit.Before;
   import org.junit.Test;
   import org.openqa.selenium.WebDriver;
   import org.openqa.selenium.chrome.ChromeDriver;
   import com.automation.pages.LoginPage;

   public class LoginTest {

       WebDriver driver;
       LoginPage loginPage;

       @Before
       public void setUp() {
           driver = new ChromeDriver();
           loginPage = new LoginPage(driver);
       }

       @Test
       public void testValidLogin() {
           driver.get("https://example.com/login");

           loginPage.enterEmail("testuser@example.com");
           loginPage.enterPassword("validPassword");
           loginPage.clickLogin();

           // Verify login is successful
           Assert.assertTrue("Login failed!", driver.getCurrentUrl().contains("dashboard"));
       }

       @Test
       public void testInvalidLogin() {
           driver.get("https://example.com/login");

           loginPage.enterEmail("invaliduser@example.com");
           loginPage.enterPassword("invalidPassword");
           loginPage.clickLogin();

           // Verify error message is displayed
           Assert.assertEquals("Invalid credentials message should be displayed", 
                               "Invalid credentials", loginPage.getErrorMessage());
       }
   }

4. **SignUpTest.java** (Test class using JUnit and Selenium):
   ```java
   package com.automation.tests;

   import org.junit.Assert;
   import org.junit.Before;
   import org.junit.Test;
   import org.openqa.selenium.WebDriver;
   import org.openqa.selenium.chrome.ChromeDriver;
   import com.automation.pages.SignUpPage;

   public class SignUpTest {

       WebDriver driver;
       SignUpPage signUpPage;

       @Before
       public void setUp() {
           driver = new ChromeDriver();
           signUpPage = new SignUpPage(driver);
       }

       @Test
       public void testValidSignUp() {
           driver.get("https://example.com/signup");

           signUpPage.enterName("John Doe");
           signUpPage.enterEmail("john.doe@example.com");
           signUpPage.enterPassword("validPassword");
           signUpPage.clickSignUp();

           // Verify sign-up is successful
           Assert.assertTrue("Sign-up failed!", driver.getCurrentUrl().contains("login"));
       }

       @Test
       public void testInvalidEmailSignUp() {
           driver.get("https://example.com/signup");

           signUpPage.enterName("John Doe");
           signUpPage.enterEmail("invalid-email");
           signUpPage.enterPassword("validPassword");
           signUpPage.clickSignUp();

           // Verify error message is displayed
           Assert.assertEquals("Please enter a valid email", signUpPage.getErrorMessage());
       }
   }

5. **pom.xml** (For Maven Project - Dependency management):
   ```xml
   <dependencies>
       <!-- Selenium -->
       <dependency>
           <groupId>org.seleniumhq.selenium</groupId>
           <artifactId>selenium-java</artifactId>
           <version>3.141.59</version>
       </dependency>
       <!-- JUnit -->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
   </dependencies>
