# REDPILL ANALYTICS PROJECT DOCUMENTATION

## Required Dependencies
* **Undetected chrome driver** - We are using undetected chromedriver to prevent browsers from being detected by bots.
* To prevent our browser being detected we have two possible approaches-
    * Make a different user agent each time.
    * Use an undetected chrome driver so that bot cannot identify the user agent every time.
* We have followed the second approach.
* **Pickle library** - We are using this library for storing website cookies.
* **Time library** - For giving sleep time so that our browser waits, whenever required.
* **Datetime library** - For datetime manipulations.
* **Pandas** - Data manipulation.
* **Boto3** - To establish connection between aws and python.
* **Apscheduler** - For setting up Scheduler
* **os and glob2** -For handling files of local directory
* **yaml module**-for handling .yml file data.
* **re module** 
 

## Approach Followed
* For the very first time we have to log in to the "**Air**" website through login credentials which are shared by the client.
* This is for saving client cookies in "**client.pkl**" format and then reuse it for multiple time login.
* We are adding these cookies to our webdriver so that we don't need to repeat login using credentials.
* Cookies allow us to login to websites without credentials.
* Using cookies we logged in to website in "**transaction history**" profile of user and download csv for sections- 
    * Completed Payouts
    * Upcoming Payouts 
    * Gross Earnings
* We are selecting data for the last one month in the "**My team transaction**" section.
* In the second sprint we scraped data for the “**Reservation**” section which contains guest user booking details. Each user has certain confirmation code associated with it and their booking details are scraped based on that.
* We are using headless mode of undetected chrome driver for hiding the browser.
* Other possible approaches-
    * Scrape data using proxy servers.
    * Scrape data using website cookies.
* We have followed the second approach in our project.

## Credentials 
* All credentials have been stored in .yml files. 
* We are loading all credentials by using .yml files.
* If number user is being increased then add their respective credentials in .yml file.

## Saving cookies
* We are saving every user cookies in form of pickle file and reuse it for multiple login.
* Each time if new user logged in try to save their cookies in pickle file for this we need to run command **python saving_cookies** and then we reuse it for multiple logins.

## cookies credentials in .yml file
* Before generating pickle file make sure cookies are cleared from web browser. Add these pickle files in .yml file.
* After generating pickle file of new user we need add that pickle file in .yml file under **user_cookies** section.
* **credentials = yaml.load(open('./filename.yml','r'),Loader=yaml.FullLoader)**
    * **pkl_file=credentials['user_cookies']['cookies_user1']**
    
## Scheduler setting up cron job
* We are adding cron job for each user credentials with their pickle file named by username.pkl. and run command python schedule.py.
    * For example-  
        * **sched.add_job(lambda: function_name('pickle_file.pkl'), 'cron', month=month, day=day, hour=hour,minute=minute)**
            * **Argument passed-**
                * **month = month in numerals**
                *    **day = day of that particular month in numerals**
                *    **hour = hour in 24-hour format in numrerals**
                *    **minute = minute in numerals**

