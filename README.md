public class QA_Automation_Assessment {
    
    // Web Login Automation using Selenium
    public static void automateWebLogin() {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        WebDriver driver = new ChromeDriver();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
        driver.manage().window().maximize();

        driver.get("https://www.saucedemo.com/");
        WebElement username = driver.findElement(By.id("user-name"));
        WebElement password = driver.findElement(By.id("password"));
        WebElement loginButton = driver.findElement(By.id("login-button"));

        username.sendKeys("standard_user");
        password.sendKeys("secret_sauce");
        loginButton.click();

        boolean isLoginSuccessful = driver.findElements(By.className("shopping_cart_link")).size() > 0;
        System.out.println(isLoginSuccessful ? "Login successful" : "Login failed");

        driver.quit();
    }

    // Automated POST API for User Management using RestAssured
    public static void automateUserManagementAPI() {
        RestAssured.baseURI = "https://fakestoreapi.com";
        RequestSpecification request = RestAssured.given();
        request.header("Content-Type", "application/json");
        
        String requestBody = "{ \"username\": \"testuser\", \"password\": \"password123\", \"email\": \"testuser@example.com\" }";
        Response response = request.body(requestBody).post("/users");

        System.out.println("Response Code: " + response.getStatusCode());
        System.out.println("Response Body: " + response.getBody().asString());
    }

    // Automated API for Transactions using RestAssured
    public static void automateTransactionAPI() {
        RestAssured.baseURI = "https://fakestoreapi.com";
        RequestSpecification request = RestAssured.given();
        request.header("Content-Type", "application/json");
        
        String requestBody = "{ \"userId\": 1, \"date\": \"2023-01-01\", \"products\": [{\"productId\": 1, \"quantity\": 2}] }";
        Response response = request.body(requestBody).post("/carts");

        System.out.println("Transaction API Response Code: " + response.getStatusCode());
        System.out.println("Transaction API Response Body: " + response.getBody().asString());
    }

    // Automated Mobile App Flow using Appium (Android)
    public static void automateMobileApp() throws MalformedURLException {
        DesiredCapabilities caps = new DesiredCapabilities();
        caps.setCapability("platformName", "Android");
        caps.setCapability("deviceName", "emulator-5554");
        caps.setCapability("app", "path/to/app.apk");
        caps.setCapability("automationName", "UiAutomator2");

        AppiumDriver<MobileElement> driver = new AndroidDriver<>(new URL("http://localhost:4723/wd/hub"), caps);
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

        MobileElement loginButton = driver.findElement(By.id("com.example.app:id/login"));
        loginButton.click();

        System.out.println("Mobile app automation completed successfully");
        driver.quit();
    }

    public static void main(String[] args) throws MalformedURLException {
        automateWebLogin();
        automateUserManagementAPI();
        automateTransactionAPI();
        automateMobileApp();
    }
}
