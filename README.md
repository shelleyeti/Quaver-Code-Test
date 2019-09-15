# New Hire Code Test
This coding challenge will be sent to potential new hires to test their debugging skills. 

# What the project does
* Uses the Github API to pull top repos.
* Loops through the top repos and grab the URLs.
* Encrypts the URLs and stores them in a text file, only if that URL does not already exist (no duplicates).
* The Github API will be called three times. In the View you will see a boolean if the text file contains any duplicates for the three API calls.

# What you need to do
* This program is broken in several places. Step through and find where the program is broken.
* The expected result is all three API call duplicate checks return false.

Remember there should be no duplicates of any URLs in the text file!

# How to deliver 
* Clone down the solution and copy the QuaverCodeChallenge folder into your own GitHub repo.
* Send us the link (email implementation@QuaverMusic.com) to your GitHub solution when complete.


## Personal Notes
1. My first attempt at running the project does not return a default view.
	- I was able to research online and look at past projects to determine that the default route in the startup file needed to be setup.
    - Setting up the routes in the controller was a more difficult process, because I wasn't sure what was missing. 
1. Now that I was able to run the program and return the view I wanted, I saw the first error hit in the GitHubService file on the GetAPI method.
    - I was able to inspect the ``content`` argument and saw that what was being returned was 'items', while the ``JObject json`` was expecting 'item'.
1. The code was still not returning the expected results, so I began to follow the code.
    - A foreach loop returned urls in uppercase``repoNames.Add((i["owner"]["url"]).ToString().ToUpper());`` while another method ReadFromFile used a while loop to return urls in lowercase `` repoNames.Add(ln.ToLower());``
    - Changing them to be the same case, allows the urls to be compared exactly
1. Since the code was still not correct, I looked at the text output file and saw 2 sets of the same encrypted urls.
    - That lead me to look at the WriteToFile method. 
    - It was writing to the output file twice because the encryption was happening inside the if statement. By moving it outside all the incoming parameters are encrypted and then compared.