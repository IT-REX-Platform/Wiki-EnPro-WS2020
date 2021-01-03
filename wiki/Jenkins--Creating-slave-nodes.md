# Creating slave nodes

Adding a slave node to Jenkins is quite simple. Just run this [script](https://github.com/IT-REX-Platform/utility-scripts/blob/main/configure-slave.sh) as root on the node. 
After that open the Jenkins dashboard and click on "Manage Jenkins" then on "Manage Nodes and Clouds" then on "New Node" or follow this [link](http://129.69.217.173:8084/computer/new). Now enter a Node name and choose "Permanent Agent" or copy an existing one.

![naming](Images/Jenkins/node-naming.png)

After that configure the node like this (You have to adjust the label and the Host address)

![configuration](Images/Jenkins/node-configuration.png)

Then click on save. And hope that nothing unforeseeable happens. Jenkins launches an agent on the node now.

![console-output](Images/Jenkins/console-output.png)

If the console output says "Agent successfully connected and online" you have done everything right. Congratulations!

![chadkins](Images/Jenkins/Chadkins.jpg)