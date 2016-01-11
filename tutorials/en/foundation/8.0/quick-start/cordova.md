---
layout: tutorial
title: Cordova end-to-end demonstration
relevantTo: [cordova]
weight: 1
---
## Overview
The purpose of this demonstration is to experience an end-to-end flow where an application &amp; an adapter are created from the MobileFirst Operations Console, and application makes a resource request call using the MobileFirst Adapter to  verify connectivity with the MobileFirst Server.

#### Prerequisites:

* Configured Xcode for iOS, Android Studio for Android or Visual Studio 2013/2015 for Windows 8/10
* MobileFirst CLI ([download]({{site.baseurl}}/downloads))
* *Optional* Stand-alone MobileFirst Server ([download]({{site.baseurl}}/downloads))

### 1. Starting the MobileFirst Server

> If a remote server was already set-up, skip this step.

From a **Command-line** window, navigate to the server's **scripts** folder and run the command: <code>./start.sh</code> in Mac and Linux or <code>start.cmd</code> in Windows.

### 2. Creating an application

In a browser window, open the MobileFirst Operations Console by loading the URL: <code>http://your-server-host:server-port/mfpconsole</code>. If running locally, use: [http://localhost:9080/mfpconsole](http://localhost:9080/mfpconsole). The username/password are *admin/admin*.
 
1. Click on the "Create new" button next to **Applications** and select the desired *platform*, *identifier* and *version* values.

    ![Image of selecting platform, and providing an identifier and version](create-an-application.png)
 
2. Click on the **Get Starter Code** tile and select to download the Cordova Starter Code.

    ![Image of creating a sample application](download-sample-application.png)
    
    ![Image of download a sample application](download-application-code.png)
 
### 3. Editing application logic

1. Open the Cordova project in your code editor of choice.

2. Select the **www/js/index.js** file and paste the following code snippet, replacing the existing `wlCommonInit()` function:

    ```javascript
    function wlCommonInit() {
        var resourceRequest = new WLResourceRequest(
            "/adapters/httpadapter/getFeed",
            WLResourceRequest.GET
        );

        resourceRequest.send().then(
            function() {
                alert("Successfully connected and retrieved data from the MobileFirst Server.");
                alert("show some server result here");
            },
            function() {
                alert ("failure");
            }
        )
    }
    ```
    
### 4. Creating an adapter

1. Click on the "Create new" button next to **Adapters** and download the **JavaScript-HTTP** adapter sample.

    > If Maven and MobileFirst CLI are not installed, follow the on-screen **Setting up your environment** instructions to install.

    ![Image of create an adapter](create-an-adapter.png)
    
    ![Image of downloading an adapter sample](download-adapter-code.png)

### 5. Editing adapter logic

1. From a **Command-line** window, navigate to the adapter's Maven project root folder and run the command: 

    ```bash
    mfpdev adapter build
    ```

2. When the build finishes, run the command:

    ```bash
    mfpdev adapter deploy
    ```

    If using a remote MobileFirst Server, run the command:

    ```bash
    mfpdev adapter deploy Replace-with-remote-server-name
    ```

### 6. Testing the application

1. From a **Command-line** window, navigate to the Cordova project root folder.
2. Run the commands: <code>cordova prepare</code> followed by <code>cordova run</code>.

 - If a device is connected, the application will be installed and launched in the device,
 - Otherwise the Simulator or Emulator will be used.

    ![Image of application that successfully called a resource from the MobileFirst Server ]()

## Next steps

- Review the [Client-side development tutorials](../../client-side-development/)
- Review the [Server-side development tutorials](../../server-side-development/)
- Review the [Authentication and security tutorials](../../authentication-and-security/)
- Review [All Tutorials](../../all-tutorials)