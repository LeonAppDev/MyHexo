---
title: AWS and Amplify
date: 2019-03-30 22:12:01
tags:
---

## Setup

I have followed amplify user guide to add a pinpoint service to AWS, and spent a lot of time investigating how to add IAM permission, and finally find out the reason I could not get permission is I need to add my credit card infromation to my account then my account could be activated. This is not reminded by error message. 

And also be aware that when you create a app using amplify, there is a configuration, that configuration usually ask your login to your amazon account, and create IAM users, when you visit the resource you created from amplify in your amazon console panel, you should use the same account, not use another account.


