package imdbMovieInfo;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.FindBy;
import org.openqa.selenium.support.How;
import org.openqa.selenium.support.PageFactory;

public class MovieDetails 
{
   WebDriver driver;
   List<WebElement> movTitleList;
   List<WebElement> movRatingList;
   List<WebElement> movRelYrList;
   
   
   
   MovieDetails(WebDriver driver)
   {
	   this.driver=driver;
   }
   
   By movTitle=By.xpath("//td[@class='titleColumn']");
   By movRatings=By.xpath("//td[@class='ratingColumn imdbRating']");
   By MovRelYr=By.xpath("//span[@class='secondaryInfo']");
   
   int i,j,k;
  
   public void getMovieDetails()
   {
	   i=j=k=0;
	   movTitleList=driver.findElements(movTitle);
	   movRatingList=driver.findElements(movRatings);
	   movRelYrList=driver.findElements(MovRelYr);
	   
	   
	   String[] tArray=new String[movTitleList.size()];
	   String[] rArray=new String[movRatingList.size()];
	   String[] yArray=new String[movRelYrList.size()];
	   
	   
	   for (WebElement data : movTitleList) 
	   {
		   tArray[i]=data.getText();
		   i++;
	   }
	   for (WebElement data : movRatingList) 
	   {
		   rArray[j]=data.getText();
		   j++;
	   }
	   for (WebElement data : movRelYrList) 
	   {
		   yArray[k]=data.getText();
		   k++;
	   }
	   
	   
		for(i=0;i<movTitleList.size();i++)
		{
			System.out.println(tArray[i]+" "+rArray[i]+" "+yArray[i]);
		}
	   
   }
	
}



//test class to launch browser and pass the driver object to the code class

package imdbMovieInfo;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;


public class BrowserLaunch {

	static WebDriver driver;
	public static void main(String[] args) throws InterruptedException 
	{
		System.setProperty("webdriver.chrome.driver", "D:\\Software\\selenium3.8.1\\chromedriver\\chromedriver.exe");
		
		driver=new ChromeDriver();
		
		//navigate to main page
		driver.get("https://www.imdb.com/");
		driver.manage().window().maximize();
		
		Thread.sleep(5000);
		//navigate to top movie rated page
		driver.findElement(By.xpath("//a[text()=' Top Rated Indian Movies ']")).click();
		Thread.sleep(5000);
		
		MovieDetails pobj=new MovieDetails(driver);
		  
		pobj.getMovieDetails();
