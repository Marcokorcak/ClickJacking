# ClickJacking Lab

Clickjacking, also known as a “UI redress attack,” is an attack that tricks a user into clicking on something
they do not intend to when visiting a webpage, thus “hijacking” the click. In this lab, I explored a
common attack vector for clickjacking: the attacker creates a webpage that loads the content of a legitimate
page but overlays one or more of its buttons with invisible button(s) that trigger malicious actions. When a
user attempts to click on the legitimate page’s buttons, the browser registers a click on the invisible button
instead, triggering the malicious action.


## Table of contents
* [Lab Setup](#Lab-Setup)
* [Task 1](#Task-1)
* [Task 2](#Task-2)
* [Task 3](#Task-3)
* [Task 4](#Task-4)
* [Task 5](#Task-5)

<img src= "https://user-images.githubusercontent.com/77298953/210186397-03d62656-e661-4a8e-b8fb-f1754ecac9da.PNG" width=70% height=70%>

## Lab Setup

The image above shows the lab environment setup by adding the DNS configurations and the websites

relating to the ip addresses in the /etc/hosts file using the command “sudo nano /etc/hosts”. Along with

this the commands “docker-compose build” and “docker-compose up” were used to start the Elgg

container. With all of this setup, all of the websites were running properly and could be visited.

## Task 1
<img src= "https://user-images.githubusercontent.com/77298953/210186455-57af4460-7c74-4718-a27c-9a8a22288f68.PNG" width=70% height=70%>

The image above shows the code that was added to the attacker.html file for the iframe

<img src= "https://user-images.githubusercontent.com/77298953/210186468-014cdc95-5e7f-4e7e-8e73-14b4a0744327.PNG" width=70% height=70%>

The image above shows the code that was added to the attacker.css file in order to position the
iframe to cover the whole page

<img src= "https://user-images.githubusercontent.com/77298953/210186483-013717a4-9f4a-4f24-9990-e773e9caaceb.PNG" width=70% height=70%>

The image above shows the iframe that was added to the www.cjlab-attacker.com website

# Explanation for Task 1
In task 1, I was tasked with adding an iframe HTML element to the www.cjlab-

attacker.com website. Along with adding the iframe, I also needed to modify the css file using the

height, width and position attributes to make the iframe cover the whole page. In order to complete

this task, I added the following code: <iframe id=“A” src=http://www.cjlab.com></iframe> into

the attacker.html file. Once this was added the iframe showed up on the attacker website, but it did

not cover the whole page. In order to make it cover the whole page, I set the position attribute to

absolute, the width and height attributes to 100% and the border attribute to none. All of this was

done in the iframe section in the attacker.css file which made the iframe cover the whole page but

I needed to clear my browsers cache and reload the website to see the changes.


Question : With the iframe inserted, what does the attacker’s website look like?

Answer: With the iframe inserted, the attacker’s website looked like the alice’s cupcakes

website except that the malicious button was at the top left of the page. This is because the

iframe along with the css attributes covered the whole page but the malicious button that was on

the page originally was not altered. The website can be seen in the image above.

## Task 2

<img src= "https://user-images.githubusercontent.com/77298953/210186642-1118d759-4b81-48f7-bad4-7f3bb41d8776.PNG" width=70% height=70%>

The image above shows that the malicious button was shifted to the position of the original
button

<img src= "https://user-images.githubusercontent.com/77298953/210186655-c9a81c16-5315-453e-94e1-1a4b2b5402b0.PNG" width=70% height=70%>

The image above shows the code that was added to the attacker.css file to shift the button
position and transparency

<img src= "https://user-images.githubusercontent.com/77298953/210186660-2b145ce7-2f57-4307-a41e-0b52a74b756d.PNG" width=70% height=70%>

The image above shows the button after making all the changes to its position and making it
transparent

<img src= "https://user-images.githubusercontent.com/77298953/210186671-a3b68180-d4c1-4133-9f53-d1a194c020bd.PNG" width=70% height=70%>

The image above shows what is displayed when the malicious button was clicked

# Explanation for Task 2
In this task, the objective was to alter the button and its position using the css file.

Before making any changes to the attacker.css file the malicious button was at the top left of the

page, but after making the changes the button was placed over the original button and made

transparent. When editing the attacker.css file, I altered the color, background-color, margin-left

and margin-right attributes. I set the color and background-color attributes to transparent so the

button would not be visible when placed over the original button and the margin-left to 50px and

the margin-top to 350px. Adding this code moved the position of the malicious button as well as

making it invisible so it would go unnoticed. After the changes the malicious button was directly

on top of the “Explore Menu” button. This allowed the clickjacking attack to carried out and

when the button was clicked the user would see the text “You Have Been Hacked!!”.


Question 2: How does the appearance of the attacker’s site compare to that of the

defender’s site?

Answer: After altering the position and css attributes of the malicious buttons, the attacker’s

website is an exact copy of the defender’s website. When looking at both websites they are

completely alike visually. The malicious button is directly on top of the “Explore Menu” button,

but it is transparent.


Question 3: What happens when you click on the “Explore Menu” button on the attacker’s

site?

Answer: When a user clicks the “Explore Menu” button on the attacker’s website, the text “You

Have Been Hacked!!” is displayed on the page. This is because the transparent malicious button

was clicked instead of the “Explore Menu” button. The image above shows this screen.


Question 4: Describe an attack scenario in which the style of clickjacking implemented for

this Task leads to undesirable consequences for a victim user.

Answer: This style of attack can impact a user in numerous ways. This can be used to forge a

POST request to alter personal information or be used to steal information from a user. An

attacker can use this method to steal machine information from a user which can reveal their

identity or location from their IP Address. This style of attack can make a script execute when

the button is clicked which can allow an attacker to gain access to a user’s machine through the

script and carry out malicious activities. There is a wide range of things that can be done through

this style of attacks.


## Task 3

The image above shows the code that was added to the index.html file

Answer: In this task, the objective was to add JavaScript code to index.html in the defender file.

I filled in the makeThisFrameOnTop() function which compared the window.top to window.self

which was done to find out if the top window and current site’s window are the same object. I

used an if statement that said if the top window is not itself, then the location of both will be

changed to be equal. Once this was done, the browser’s cache was cleared, and I had to reload

the page in order for the changes to take effect. This is a frame-busting script that prevents

malicious webpages from being displayed using a iframe.

Question 5: What happens when you navigate to the attacker’s site now?

Answer: After implementing this code, when I visited the attacker’s website, I am redirected to

the defender website. The url of the website changes to www.cjlab.com. Adding this JavaScript

code and function prevented the attacker’s website from being displayed within an iframe. This

was done as a countermeasure to prevent websites from opening the webpage within an iframe as

well as preventing buttons on the attacker’s webpage from being overlaid on top of it.

Question 6: What happens when you click the button?

Answer: When the button is clicked, the website refreshes and redirects the user to the

defender’s website. This can be seen by the url that is displayed after clicking the button which is

the defender websites url. This occurs because of the JavaScript function and code that was

implemented in this task. The code prevented buttons on the attacker’s webpage from being

overlaid on top of the defender website.

## Task 4

The image above shows the code that was added to the attacker.html file

The image above shows the result when the button was clicked on the attacker’s website

Answer: In this task, the objective was to implement code in the attack.html file that would work

around the previous code implemented in the previous task on the defender’s website. In the task

I added the sandbox attribute to the iframe code, and this attribute added an extra set of

restrictions for the content in the iframe. The sandbox attribute treats the content in the iframe as

being from a unique origin and allow scripts to be run. Allowing scripts to run enabled the

malicious button to work properly once again.

Question 7: What does the sandbox attribute do? Why does this prevent the frame buster

from working?

Answer: The sandbox attribute applies or lifts restrictions to the content in the iframe. Sandbox

was specifically used in this task to prevent the frame buster code from working. Sandbox

relaxes the restrictions set to the content of the iframe by the frame buster code and permits

scripts to execute. Allowing scripts to be executed, the malicious attack can now be carried out

again.

Question 8: What happens when you navigate to the attacker’s site after updating the

iframe to use the sandbox attribute?

Answer: After implementing the sandbox code, the attacker’s site now works as intended. The

attacker’s website is shown instead of the defender’s website. This is due to the sandbox attribute

which allows the contents of the iframe to be displayed as intended.

Question 9: What happens when you click the button on the attacker’s site?

Answer: When the malicious button is clicked, the text “You Have Been Hacked!!” is displayed,

showing that the sandbox attribute worked around the frame buster code.

## Task 5

The image above shows the code that was added to the apache_defender.conf file

The image above shows the error code that is thrown when the attacker’s website is visited

Answer: The objective of this task was to modify the defender’s response headers in the Apache

configuration file. In order to edit this file, I first needed to get to the image_defender directory

and then edit the apache_defender.conf file. Once I was in the file I added X-Frame-options

header to the value “DENY” and added the Content-Security-Policy (CSP) header to contain the

directive “frame-ancestors ‘none’ “. Adding these header options prevented the attacker’s

website from being loaded due to the website not meeting header requirements to load the

defender website in the iframe. This result was gotten once I restarted as well as re-built the

docker containers to update all information. The screen printed “Firefox Can’t Open This Page”.

Questions 10: What is the X-Frame-Options HTTP header attribute, and why is it set to

“DENY” to prevent the attack?

Answer: The X-Frame-Attribute option on the HTTP header attribute is used to allow content

publishers to prevent their own content from being used in an iframe by attackers. The “DENY”

option was used to prevent any use of the defender’s website in an iframe. This option means

that the defender’s website cannot be displayed in a frame regardless of what the website is

attempting to do.

Question 11: What is the Content-Security-Policy header attribute, and why is it set to

“frame-ancestors ‘none’ ” to prevent the attack?

Answer: The Content-Security-Policy header of frame ancestor’s attribute specifies valid parents

that may embed a page using a frame. This allows website to specify what parent source may

embed a page and since we have it set to none, this means that the URI cannot be framed inside

an iframe tag. This is similar to setting X-Frame-Options to deny since it prevents the framing of

the defender’s website.

Question 12: What happens when you navigate to the attacker’s site after modifying each

response header (one at a time)? What do you see when you click the button?

Answer: When I visit the attacker’s website with both response headers implemented the

website will not load. An error message is displayed saying “www.cjlab.com will not allow

Firefox to display the page if another site has embedded it”. This means that the response

headers worked properly and prevented the website from being displayed and possibly attracting

victims. When modify the apache file so that only one response header is active at a time, the

result is still the same. When I run the file with just X-Frame-Options the webpage will not load

and when I run just the CSP attribute, the webpage will also not load. This is because both

header attributes serve the same purpose, preventing the iframe from being loaded with the

defender’s website. When clicking the “Open Site in New Window” option on the attacker

website, the website refreshes back to the defender’s website.
