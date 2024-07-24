---
layout: post
title: "Setting up Selenium in Visual Studio Code on MacOs with Apple Chip M1"
date: 2021-11-03 19:08:30 -0400
categories: QA
tags: [Selenium]
years: ['2021']
comments: true
---

I use MacBook Pro 2020 with chip Apple M1, and was not sure if it is compatible with Selenium, a QA automation testing tool. I also would like to use it with Visual Studio Code, a popular choice of text editior and IDE. I had to google up and this website below is the best choice to follow through. 

https://funnelgarden.com/setup-selenium-with-java-on-visual-studio-code/


# What do I need beforehand?

- [Visual Studio Code][Visual Studio Code] or also known as VS Code
- Latest Java version from [Oracle][Oracle] 
- Java Extension Pack in VS Code
- [Selenium][Selenium] WebDriver
- [ChromeDriver][ChromeDriver] 


## 1) Let's start with Visual Studio Code

I installed [Visual Studio Code][Visual Studio Code] when I first got this laptop awhile ago, because I read that it is the best text editor to have and it is already an IDE, or `integerated development environment`. It allows different developer tools to work together. It debugs and does many other wondrous things.

I don't remember exactly the steps of installing Visual Studio Code, but I think it should be simple. Click on this [Visual Studio Code][Visual Studio Code] and scroll all way down to the bottom until you see this image:

![VS-ARM](/public/img/VS-ARM.png)

Click on `Apple Silicon` to install the VS Code, <strong>again this is for MacBook Pro with chip `Apple M1` </strong> or what I usually see `ARM 64` for different downloads.

## 2) The next step, download Java for MacOS M1 Chip

The thing to know, MacBook Pro with Apple M1 chip doesn't come with Java, you could check by typing `java -version` in terminal. So we will need to download Java from [Oracle][Oracle]. I created a short video clip below of how to install Java quickly. I already installed and don't want to reinstall. Just follow through without cancelling unless you feel necessary.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ABbsylwIlF4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> 
 <br>
After installing Java SDK, open up terminal and then type either `java -version` or `javac -version` and it should show the version. `Javac` is java complier.  I forgot to add, it is possble to open up terminal in Visual Studio Code. I use terminals in Visual Studio Code to stay focused on whatever the projects I am working on. Visual Studio Code is changing things, more conventional. 

## 3) Add Java Extension Pack in VS Code

![JEPVS](/public/img/JEPVS.jpg)

I find it easier to add the package from in VS Code application. Please check the video below on how to add an extension in Visual Studio Code application. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/ver8fQNSXMM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 <br>
I am basically repeating what https://funnelgarden.com/setup-selenium-with-java-on-visual-studio-code/ suggested on doing. I would suggest to create a project folder in finder first. I created "Selenium" folder to prepare for installing all tools inside for broad use, and then specific projects will be subfolders. 

Open up Visual Studio Code, click on explorer which has a icon of two files on upper left corner, and then click "Create Java Project" button on the bottom. 

![java_project](/public/img/java_project.png){:height="500px" width="auto"}

Dropdown box will ask for which project type. Pick "No build tools". After that, it will pop up Mac's Finder application asking where you want to place your project in. I created a subfolder "firstTest" in "Selenium" folder.

![no_build_tools](/public/img/no_build_tools.png)

VS Code should create a new project with src folder with "Hello, World!" file and a Readme.

![example](/public/img/example.png)

## 4) Installing Selenium WebDriver

What is [Selenium][Selenium]? It is a QA automation tool used to test browsers and web application. Currently there's a great demand for it. Click on this link [Selenium][Selenium] and click on `Downloads` in the menu bar on the top. Scroll down to the java links and pick the stable one.

![selenjava](/public/img/selenjava.png){:height="auto" width="50%"}

After downloading the stable zip file, open two finders. One in Downlaods folder and another where the project folder might be at. Create another folder "jars and drivers" in the project folder for. Open the zip and extract all `.jars` files and move over to project folder in Selenium folder. 

[Visual Studio Code]:https://code.visualstudio.com/
[Oracle]:https://www.oracle.com/index.html
[Selenium]:https://selenium.dev
[ChromeDriver]:https://chromedriver.chromium.org/downloads
