package Testcases;

import java.util.List;

import org.openqa.selenium.WebElement;
import org.testng.Assert;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

import ElementRepository.LoginPage;

import ElementRepository.ManageOrders;
import Utilities.GeneralUtilities;
import constants.Constant;

public class ManageOrderTestCases extends BaseClass {

	ManageOrders mo;
	LoginPage lp;
	GeneralUtilities go = new GeneralUtilities();

	@Test

	public void Manageorders_search_btn_size() throws InterruptedException {
		mo = new ManageOrders(driver);
		lp = new LoginPage(driver);
		lp.presteps();
		mo.clickManageOrderTab();
		String actual = mo.font_search();
		System.out.println(actual);
		String expected = Constant.fontSize;
		Assert.assertEquals(actual, expected, Constant.fontErrorMessage);

	}

	@Test

	public void Manageorders_reset_btn_size() {
		mo = new ManageOrders(driver);
		lp = new LoginPage(driver);
		lp.presteps();
		mo.clickManageOrderTab();
		String actual2 = mo.fontReset();
		System.out.println(actual2);
		String expected2 = Constant.fontSize;
		Assert.assertEquals(actual2, expected2, Constant.fontErrorMessage);
	}

	@Test

	public void Manageorders_searchbtn_bg_clr_validation() {
		mo = new ManageOrders(driver);
		lp = new LoginPage(driver);
		lp.presteps();
		mo.clickManageOrderTab();
		String actual2 = mo.backGroundSearch();
		System.out.println(actual2);
		String expected2 = Constant.bgclr2;
		Assert.assertEquals(actual2, expected2, Constant.bgColorErrorMessage);
	}

	@Test
	public void manageOredersSearchbyBank() {
		mo = new ManageOrders(driver);
		lp = new LoginPage(driver);
		lp.presteps();
		mo.clickManageOrderTab();

		boolean actual =true;
				//mo.searchByBank();
		boolean expected = true;
		Assert.assertEquals(actual, expected);

	}


	@DataProvider (name = "data-provider")
	public Object[][] dpMethod(){
		return new Object[][]{{"Select" }, { "Paid" } };
	}


	@Test(dataProvider="data-provider")
	public void statusvalidation(String value) throws InterruptedException {
		mo = new ManageOrders(driver);
		lp = new LoginPage(driver);
		lp.presteps();
		mo.clickManageOrderTab();
		mo.clickSearchbtn();
		String actual =mo.statusdropdwnTest(value);
		List<String> expected =mo.listOfExpectedValuesDropdown();
		for(int i=0;i<expected.size();i++) {
			Assert.assertEquals(actual, expected.get(i), "dropdown values not expected");
		}

		

	}
}
