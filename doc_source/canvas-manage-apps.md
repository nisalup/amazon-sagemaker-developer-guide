# Manage apps<a name="canvas-manage-apps"></a>

The following sections describe how you can manage your SageMaker Canvas applications\. You can view, delete, or relaunch your apps from the **Domains** section of the SageMaker console\.

## Check for active apps<a name="canvas-manage-apps-active"></a>

To check if you have any actively running SageMaker Canvas apps, use the following procedure\.

1. Open the [SageMaker console](https://console.aws.amazon.com/sagemaker/)\.

1. In the navigation pane, select **Domains**\.

1. On the **Domains** page, choose your Domain\.

1. On the **Domain details** page, under **User profiles**, select the user profile name for the Canvas application that you want to view\.

1. Under **Apps**, find the app that says **Canvas** in the **App type** column\.

The **Status** column displays the status of the app, such as **Ready**, **Pending**, or **Deleted**\. If the app is **Ready**, then your SageMaker Canvas session is active\. You can delete the app from the console or log out from the SageMaker Canvas interface to stop the session\.

## Delete app<a name="canvas-manage-apps-delete"></a>

If you want to end your SageMaker Canvas session, you can either log out from the SageMaker Canvas application or delete your application from the SageMaker console\. A *session* is the period of time from when you start using SageMaker Canvas to the point when you stop using it\. Deleting the application only ends the session\. Models and datasets aren’t affected, but Quick build tasks automatically restart when you log in again\. The billing for the session also stops\. 

Use the following procedure to delete your SageMaker Canvas application\.

1. Open the [SageMaker console](https://console.aws.amazon.com/sagemaker/)\.

1. In the navigation pane, select **Domains**\.

1. On the **Domains** page, choose your Domain\.

1. On the **Domain details** page, under **User profiles**, select the user profile name for the Canvas application you want to view\.

1. Under **Apps**, find the application that says **Canvas** in the **App type** column\.

1. In the **Action** column, choose **Delete app**\.

1. In the **Delete app** dialog box, select the **Yes, delete app** prompt, confirm the deletion by typing **delete** in the text field, and then choose **Delete**\.

After you've successfully deleted the application, the **Status** column says **Deleted**\. Otherwise, your application is still active\.

You can also end the session by [logging out](canvas-log-out.md) from within the SageMaker Canvas application\.

## Relaunch app<a name="canvas-manage-apps-relaunch"></a>

If you delete or log out of your SageMaker Canvas application and want to relaunch the application, use the following procedure\.

1. Navigate to the [SageMaker console](https://console.aws.amazon.com/sagemaker/)\.

1. In the navigation pane, choose **Canvas**\.

1. On the SageMaker Canvas landing page, in the **Get Started** box, select your user profile from the dropdown\.

1. Choose **Open Canvas** to open the application\.

SageMaker Canvas begins launching the app\.

You can also use the following secondary procedure if you encounter any issues with the previous procedure\.

1. Open the [SageMaker console](https://console.aws.amazon.com/sagemaker/)\.

1. In the navigation pane, select **Domains**\.

1. On the **Domains** page, choose your Domain\.

1. On the **Domain details** page, under **User profiles**, select the user profile name for the SageMaker Canvas application you want to view\.

1. Choose **Launch** and select **Canvas** from the dropdown list\.

SageMaker Canvas begins launching the app\.