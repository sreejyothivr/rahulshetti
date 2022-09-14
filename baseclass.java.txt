package Testcases;

import java.io.FileInputStream;

import java.io.IOException;
import java.time.Duration;
import java.util.Properties;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.ITestResult;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Parameters;

import Utilities.Screenshotcapture;

public class BaseClass {
	Screenshotcapture sc;
	public static Properties prop;
	WebDriver driver;

	public static void testBasic() throws IOException {
		prop = new Properties();
		FileInputStream fileIO = new FileInputStream(
				System.getProperty("user.dir") + "\\src\\main\\resources\\Properties\\Config.properties");
		prop.load(fileIO);
	}

	@Parameters("Browser")
	@BeforeMethod(alwaysRun = true)
	public void beforemethod(String browser) throws IOException {
		if (browser.equals("chrome")) {

			testBasic();
			System.setProperty(prop.getProperty("chromeBrowserDriver"),
					System.getProperty("user.dir") + prop.getProperty("chromeDriverPath"));

			driver = new ChromeDriver();
			driver.get(prop.getProperty("baseURL"));
			driver.manage().window().maximize();
			driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
		}

		else if (browser.equals("firefox")) {
			testBasic();
			System.setProperty(prop.getProperty("fireFoxBrowserDriver"),
					System.getProperty("user.dir") + prop.getProperty("fireFoxBrowserDriverPath"));

			driver = new FirefoxDriver();
			driver.get(prop.getProperty("baseURL"));
			driver.manage().window().maximize();
			driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
		} else {
			testBasic();
			System.setProperty(prop.getProperty("edgeBrowserDriver"),
					System.getProperty("user.dir") + prop.getProperty("edgeDriverPath"));

			driver = new EdgeDriver();
			driver.get(prop.getProperty("baseURL"));
			driver.manage().window().maximize();
			driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
		}
	}

	@AfterMethod(alwaysRun = true)
	public void aftermethod(ITestResult iTestResult) throws IOException {

		if (iTestResult.getStatus() == iTestResult.FAILURE) {
			sc = new Screenshotcapture();
			sc.Screenshotcapturefunc(driver, iTestResult.getName());

	}
		 driver.close();

	}
}
