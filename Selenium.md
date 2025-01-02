import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import pytest


@pytest.fixture(scope="module")
def driver():
    driver = webdriver.Chrome(executable_path='/path/to/chromedriver')  
    driver.get("https://www.lambdatest.com/selenium-playground/table-sort-search-demo")
    yield driver
    driver.quit()

def test_search_table(driver):
  
    search_box = driver.find_element(By.ID, "task-table-filter")
    search_box.clear()  
    search_box.send_keys("New York")
    search_box.send_keys(Keys.RETURN)

 
    time.sleep(2)  
    
    
    rows = driver.find_elements(By.XPATH, "//table[@id='task-table']//tbody//tr")
    total_entries = len(rows)
    
        assert total_entries == 5, f"Expected 5 entries, but found {total_entries} entries."
    print(f"Test Passed! Found {total_entries} entries matching 'New York'.")


if __name__ == "__main__":
    pytest.main()
