
# Getting Started with CSE 15L

---	
This page will help you navigate through the inital phases of CSE 15L by telling you how to get started and set up the environment for this course. This page contains 
details about the following:
* *Installing VSCode*
* *Establising a Remote Conenction*
* *Trying out Commands on the Terminal*

---	

## Installing VSCode
* Go to [https://code.visualstudio.com/download](https://code.visualstudio.com/download). 
 
  <img width="945" alt="image" src="https://user-images.githubusercontent.com/63532613/211911901-36e41b91-c32c-4e7b-b6a0-d75e678f7551.png" class = "center">
  
* Based on your operating system, click the download button to install the latest version of VSCode on your system.
 
  <img width="953" alt="image" src="https://user-images.githubusercontent.com/63532613/211923443-b8a2e4f5-51cf-4cab-906f-0dc74f91dca9.png">
  
* Once the installation process is complete, launch the .exe file by clicking on it.

* A popup will show up, which will give you the option to modify any installation settings. You should be fine even if you just click next for each of the settings to go with the default setup.

* That's it! Now you have your text editor set up!

  <img width="945" alt="image" src="https://user-images.githubusercontent.com/63532613/211912904-6b55a021-e375-43ac-a09d-001d0b92a1cc.png" class = "center">

---	

## Establising a Remote Conenction

In CSE 15L, we have a course specific account. We will use this account and the VSCode terminal in order to establish a remote connection so that we can perform various tasks over the internet.

* The first step is to install git.
    * Check if git is already installed on your machine by typing out `git --version` on the VSCode terminal. If git is already installed, you should get a response as shown in the image below.
   
    * If git is not installed, go to [https://gitforwindows.org/](https://gitforwindows.org/) and click on the download button. Follow the instructions as they appear to set up git. Once done, you can run `git --version` to confirm whether git has been installed.
    
    <p align="center">
          <img width="290" alt="image" src="https://user-images.githubusercontent.com/63532613/211924652-bfa4da35-2931-47c1-a5b6-12d177e55a23.png">
   </p>

* Set up bash on the VSCode terminal by following the instructions present on the following link: [Bash Setup]([https://gitforwindows.org/](https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal/50527994#50527994))

* Run the following command on the VSCode terminal.

  `ssh cs15lwi23<???>@ieng6.ucsd.edu`
  
Complete the part that says `???` looking at the username of your CSE 15L account. This information can be found on  [Educational Technology Services](https://sdacs.ucsd.edu/~icc/index.php).

* when you receive the prompt that says `Are you sure you want to continue connecting (yes/no/[fingerprint])?`, type yes and press enter. Then, enter your password when prompted to do so. You will get the following message when the remote connection has been established successfully.

  <p align="center">
    <img width="322" alt="image" src="https://user-images.githubusercontent.com/63532613/211927938-c6c027f5-01b1-4562-a2a7-527a2a8fd29e.png">
  </p>

---	

## Trying out Commands on the Terminal

Now that you have set up the Visual Studio code and established a remote connection, it is now time to try out some commands. The following are some of the commands you can execute:

* ```pwd```
This command can be used to print the working directory so that users get to know which folder they are currently in.

```
[cs15lwi23aaq@ieng6-203]:~:88$ pwd
/home/linux/ieng6/cs15lwi23/cs15lwi23aaq
```

* ```ls```
This command can be used to list the files and folders that are present in the current directory. Users can either run these files or navigate into certain folders as per their requirements.

```
[cs15lwi23aaq@ieng6-203]:~:89$ ls
perl5  wavelet
```

* ```ls -a```
This command is used to list all the files and folders that are present in the current directory, even the hidden ones!

```
[cs15lwi23aaq@ieng6-203]:~:90$ ls -a
.   .bash_history  .bashrc  .config  .kshrc  .locallogin  .modulesbegenv  .pki         .profile   .zshenv  perl5
..  .bash_profile  .cache   .cshrc   .local  .login       .motd           .procmailrc  .zprofile  .zshrc   wavelet
```

* ```ls -lat```
Want to access more information about the files and folders present in this directory? You can use this command to achieve your goal. It will give you all the information you need about the user, host, and time of creation for each of the files and folders.

<p align="center">
      <img width="354" alt="image" src="https://user-images.githubusercontent.com/63532613/214352925-147327ef-1d35-4c83-a7db-474a71830834.png">
  </p>

* ```cd```
Now that you know how to check the directory you are currenly in, you may wonder how you can move over to some other directory to access files and folders that are present there. The cd command stands for "change directory," and can help you do the same.

```
[cs15lwi23aaq@ieng6-203]:~:92$ cd wavelet
[cs15lwi23aaq@ieng6-203]:wavelet:93$ pwd
/home/linux/ieng6/cs15lwi23/cs15lwi23aaq/wavelet
```

* ```cat <fileName>```
This command can be used to print the contents of any text based file to the terminal. It's quite interesting that we can even print out the contents of a `.java` file since it is also a form of a text file at the end of the day. Moreover, we can print the conent of multiple files as well by separating the file names using spaces.

  <p align="center">
      <img width="458" alt="image" src="https://user-images.githubusercontent.com/63532613/214354462-b72c7e8a-6ab4-4a05-8688-565a4a0c8a39.png">
  </p>

  
<ins>*Challenge Question*</ins>
  
*Try to find a file called perl5 and use the cd command to reach it. To verify if you have been able to reach the file use the `pwd` command*
  
<ins>*Answer*</ins>

<p align = "center">
  <img width="214" alt="image" src="https://user-images.githubusercontent.com/63532613/214354766-64f3a686-4159-45f6-b0ed-5f0bb80fb436.png">
 </p>
  
 ---	
