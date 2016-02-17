# Scrolling a WebElement Into View
_02/16/2016_

Recently, I have been working quite a bit with [Selenium/TestNG](http://testng.org/doc/selenium.html).
While writing a test class, I ran into an issue where an iFrame that was fixed to
the bottom of the window had a high z-index and was covering an element that needed
to be targeted and clicked using Selenium.  There's a simple solution for cases
such as this (example in Java, but the idea is language agnostic).

```java
WebElement element = driver.findElement(By.cssSelector(".your-css-selector-here"));
((JavascriptExecutor) driver).executeScript("arguments[0].scrollIntoView(true);", element);
Thread.sleep(500);
```

Thank you to [this](http://stackoverflow.com/a/20487332/2824419) helpful StackOverflow post.
