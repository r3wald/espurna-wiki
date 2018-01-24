Do you want to do a pull request?

First things first: **THANK YOU!**. ESPurna started as a personal project and it will be great it becomes a community project. There are som many things that can be improved, added and fixed (yeah, a lot a small bugs and not so small bugs there, I'm sure). And sometimes I just don't have the time to work on it as much as I'd like to. 

Second. Let's try to keep it homogeneous and readable. I have my coding style. It's mostly standard but sometimes it can be opinionated. It you are willing to do a pull request, there are a few things I would ask you first:

## Pull request ##
* Do the pull request against the **`dev` branch**
* **Only touch relevant files** (beware if your editor has auto-formatting feature enabled)
* If you are adding a new functionality (new hardware, new library support) not related to an existing component move it to it's own modules (.ino file)

## Coding style ##
* This project uses **4 space indentation**, not tabs
* **Class names** are UpperCamelCased
* **Method names** are lowerCamelCased
* **Variables** are underscored_lower_case (I know, I don't always follow this rule myself)
* **Private methods** and variables (even if private to the module they are declared on) are "_"-leaded
* **Function starting bracket** is in the same line as the method declaration

I know current code does not always follow these rules. I'm fixing it as I rework each of the modules.

And thank you again!