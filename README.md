# Alerting Hands On

## 1. Log into the Environment
Sign into your workshop cloud instance. Details of your login credentials and should have been emailed to you. 

## 2. Head to the Alerting Section
On the left sidebar go to Alerts and IRM --> Alerting --> Alert Rules

![image](https://github.com/user-attachments/assets/f874d022-8d4b-4903-883f-ed03ca9a9e1d)

## 3. Define our Alert Condition: 
  3.1 Enter an Alert rule name. To Differentiate from others use the formatting of ```{{initials}}-TestAlert```. ex: ```MC-TestAlert```
  3.2 Define query and Alert Condition. Copy and paste in the query: 
  ```
    histogram_quantile(0.95, sum(rate(traces_spanmetrics_latency_bucket{span_kind=~"SPAN_KIND_SERVER|SPAN_KIND_CONSUMER", job="ditl-demo-prod/checkoutservice", deployment_environment=~".*"} [$__rate_interval])) by (le,job)) * 1000
  ```
 This query is telling us the latency in MS of a service called ```checkoutservice```

 Click ```Run Query``` after you've added it in so you can see the current latency. 

 ![image](https://github.com/user-attachments/assets/8f0992e5-a000-4fd8-b8d7-fcde59e290c6)


 3.3 Let's play around with the alert condition. By Default it is saying If above 0 fire the alert, in this case that will make the alert always be firing. 

Set it to ```800``` and click ```Preview alert rule condition``` to see that the alert rule preview no longer shows it firing since the current latency is below 800. 

Set it to a lower number, like 100 so we can test out it actually firing to us. 

![image](https://github.com/user-attachments/assets/494ffdc1-637b-4bfb-8886-e00570fb5ef9)


## 4. Add Folder and labels
  4.1 Create a New Alert folder with your name. Folders are just used for Organization in the UI. 
  4.2 Optionally, add some Labels. 
  
  ![image](https://github.com/user-attachments/assets/8ca83637-9bdc-4bd4-b465-bfbfc8df8657)

## 5. Set Evaluation Behavior 

