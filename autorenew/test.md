---
title: Testing the Function
description: Testing the RCL AutoRenew Function
parent: AutoRenew Function
nav_order: 4
---

## Testing the AutoRenew Function
**V6.0.10**

In this section, you will learn how to test the RCL AutoRenew function.

- In the Azure portal, open the function app and open the 'Functions'

- Then, open the 'Certificate-Test' function

![install](../images/autorenew_test/func.PNG)

- In the **Certificate-Test** function, click on 'Code + Test', and expand the 'Logs' window

- Get the **function Url**

![install](../images/autorenew_test/func2.PNG)

- Paste the function url in a browser

- You should see the output of the function in the browser similar to the one shown below. 

![install](../images/autorenew_test/func3.PNG)

- You should see the output of the function in the logs window similar to the one shown below.

![install](../images/autorenew_test/func4.png)

- Please ensure that there are no errors in the log. If there are errors, the function is misconfigured and certificate renewal will fail.

**Note: The 'Certificate-Renew-Automatic' function will automatically run on a weekly basis and automatically renew certificates that are about to expire. There is no need to manually run the function apart from manual testing**

## Related Articles

- [Installing AutoRenew Function](./installation.md)
- [Configuring AutoRenew Function](./configure.md)






