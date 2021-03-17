using NUnit.Framework;
using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using System;

public class SeleniumTests
{
    IWebDriver driver;

    [SetUp]
    public void Setup()
    {
        driver = new ChromeDriver();
    }

    [TearDown]
    public void TearDown()
    {
        driver.Quit();
    }

    [Test]
    public void Test_SearchforQAinWikipedia()
    {
        driver.Url = "https://wikipedia.org";
        driver.FindElement(By.CssSelector("input#searchInput")).Click();
        driver.FindElement(By.CssSelector("input#searchInput")).SendKeys("QA");
        driver.FindElement(By.CssSelector("input#searchInput")).SendKeys(Keys.Enter);
        Assert.AreEqual("https://en.wikipedia.org/wiki/QA", driver.Url);
    }

    [Test]
    public void Test_AddTwoNumbers_Valid()
    {
        driver.Url = "https://sum-numbers.nakov.repl.co";
        driver.FindElement(By.CssSelector("input#number1")).SendKeys("15");
        driver.FindElement(By.CssSelector("input#number2")).SendKeys("7");
        driver.FindElement(By.CssSelector("#calcButton")).Click();
        var resultText = driver.FindElement(By.CssSelector("#result")).Text;
        Assert.AreEqual("Sum: 22", resultText);
    }

    [Test]
    public void Test_AddTwoNumbers_InvalidInput()
    {
        driver.Url = "https://sum-numbers.nakov.repl.co";
        driver.FindElement(By.CssSelector("input#number1")).SendKeys("hello");
        driver.FindElement(By.CssSelector("input#number2")).SendKeys("");
        driver.FindElement(By.CssSelector("#calcButton")).Click();
        var resultText = driver.FindElement(By.CssSelector("#result")).Text;
        Assert.AreEqual("Sum: invalid input", resultText);
    }

    [Test]
    public void Test_AddTwoNumbers_Reset()
    {
        driver.Url = "https://sum-numbers.nakov.repl.co";

        // Fill the form and assert all fields are not empty
        driver.FindElement(By.CssSelector("input#number1")).SendKeys("5");
        driver.FindElement(By.CssSelector("input#number2")).SendKeys("10");
        driver.FindElement(By.CssSelector("#calcButton")).Click();
        var num1Text = driver.FindElement(By.CssSelector("input#number1")).GetAttribute("value");
        Assert.IsNotEmpty(num1Text);
        var num2Text = driver.FindElement(By.CssSelector("input#number2")).GetAttribute("value");
        Assert.IsNotEmpty(num2Text);
        var resultText = driver.FindElement(By.CssSelector("#result")).Text;
        Assert.IsNotEmpty(resultText);

        // Fill the form and assert all fields are empty
        driver.FindElement(By.CssSelector("#resetButton")).Click();
        num1Text = driver.FindElement(By.CssSelector("input#number1")).GetAttribute("value");
        Assert.AreEqual("", num1Text);
        num2Text = driver.FindElement(By.CssSelector("input#number2")).GetAttribute("value");
        Assert.AreEqual("", num2Text);
        resultText = driver.FindElement(By.CssSelector("#result")).Text;
        Assert.AreEqual("", resultText);
    }

    [Test]
    public void Test_GoogleSearch_Selenium()
    {
        driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(5);

        // Navigate to Google
        driver.Url = "https://google.com";

        // Hide the "Terms of Service" popup box. First go to the <iframe> holding the popup
        driver.SwitchTo().Frame(0);

        // Wait for the [Agree] button to appear on the page and click it
        driver.FindElement(By.CssSelector("#introAgreeButton"));
        var agreeButton = driver.FindElement(By.CssSelector("#introAgreeButton"));
        agreeButton.Click();

        driver.SwitchTo().Window(driver.WindowHandles[0]);

        // Search for "Selenium"
        var queryInput = driver.FindElement(By.CssSelector("input[name=q]"));
        queryInput.Click();
        queryInput.SendKeys("Selenium");
        queryInput.SendKeys(Keys.Enter);

        // Open the first search result
        var firstLink = driver.FindElements(By.CssSelector(".g a"))[0];
        firstLink.Click();

        // Assert that the site open is "https://www.selenium.dev/" with the correct window title
        Assert.AreEqual("https://www.selenium.dev/", driver.Url);
        Assert.AreEqual("SeleniumHQ Browser Automation", driver.Title);
    }

}
