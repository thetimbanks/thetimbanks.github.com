---
author: tpb976
comments: true
date: 2010-01-16 17:17:49+00:00
layout: post
slug: windows-7-login-failed-for-user-iis-apppooldefaultapppool
title: Windows 7 Login failed for user "IIS APPPOOL\DefaultAppPool"
wordpress_id: 69
categories:
- Microsoft
---

While starting development on a new project in Windows 7, I ran across the following error when trying to access the database.

    
    <em><em>Cannot open database "<Database Name>" requested by the login. The login failed.
    Login failed for user 'IIS APPPOOL\DefaultAppPool'.
    
    </em></em><em><em> </em></em>


I initially Googled the error and found this [forum post](http://www.codetoday.net/default.aspx?g=posts&t=1595) that helped me solve the problem.  The site is in some other language so I will go over what you need to do here.

First, find the site that your application running under in IIS.

[![](http://thetimbanks.com/wp-content/uploads/2010/01/SelectSite.png)](http://thetimbanks.com/wp-content/uploads/2010/01/SelectSite.png)

Select the site and click on "Advanced Settings" in the column on the right.  See which Application Pool your site is running under.

[![](http://thetimbanks.com/wp-content/uploads/2010/01/AdvancedSettings-300x174.png)](http://thetimbanks.com/wp-content/uploads/2010/01/AdvancedSettings.png)

Now, click on "Application Pools" in IIS and select the application pool that your site is running under.  Click on "Advanced Settings".

[![](http://thetimbanks.com/wp-content/uploads/2010/01/AppPool-300x79.png)](http://thetimbanks.com/wp-content/uploads/2010/01/AppPool.png)

Scroll down to the "Process Model" section and click on the identity field.  Once it is selected, click on the "ellipsis" button.  In the dropdown under "Built-in Account" select "LocalSystem".

[![](http://thetimbanks.com/wp-content/uploads/2010/01/Identity-251x300.png)](http://thetimbanks.com/wp-content/uploads/2010/01/Identity.png)
