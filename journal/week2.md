# Week 2 — Distributed Tracing  
This week I worked on **Instrumentation and observability** of our app.  
I configured the backend flask application to use Open telemetry(OTEL) with Honeycomb.io as the provider.  
I created honey comb environment which gave us an API key
we set our environment using the key obtained from
honeycomb and we set it such that it runs next time we boot up.
What I learn there is that we don't want to set our environment in honeycomb to be system _ wide because we could have multiple applications reporting to honeycomb within same container. Rather we hardcoded it into our docker_ compose Yml file.
we set the OTEL service name: Backend-flask
I also learnt that our whole project has to have the same 
Honeycomb API keys so that all the little pieces of Stories 
From the different servies can be pieced together.
Each piece of the project must have it's own service name .

Distributed tracing ( Honeycomb ) can also be implemented seperately for frontend.

All we have done sofar is that we are configuring OTEL (open telemetry) to be able to send data to honeycomb by installing the Open telemetry libraries needed
we added files to the requirement . txt file for the backend.  
Imported opentelemetry files for app.py
- Run queries to explore traces within Honeycomb.io.  
![Screenshots of queries in Honeycomb.io](https://github.com/brahm0/aws-bootcamp-cruddur-2023/blob/36b277948a55133a4f766ca47cc4fb0bc8af696f/_docs/assets/Honeycomb%20query.png).  

- Instrument AWS X-Ray into backend flask application.  

- Configure and provision X-Ray daemon within docker-compose and send data back to X-Ray API.  

- Observe X-Ray traces within the AWS Console.  

- Integrate Rollbar for Error Logging.  

- Trigger an error an observe an error with Rollbar.  
![Screenshots of triggered errror](https://github.com/brahm0/aws-bootcamp-cruddur-2023/blob/8c1dec89db0be431db0dbec97ddffd1f551cc92a/_docs/assets/Rollbar%20Error%20capture%201.png)![2](https://github.com/brahm0/aws-bootcamp-cruddur-2023/blob/8c1dec89db0be431db0dbec97ddffd1f551cc92a/_docs/assets/Rollbar%20Error%20capture%202.png)![3](https://github.com/brahm0/aws-bootcamp-cruddur-2023/blob/8c1dec89db0be431db0dbec97ddffd1f551cc92a/_docs/assets/Rollbar%20Error%20capture%203.png)  

- Install WatchTower and write a custom logger to send application log data to CloudWatch Log group.  

## HOMEWORK ##  
### Add custom instrumentation to Honeycomb to add more attributes eg. UserId, Add a custom span ###   

I created a custom span by hardcoding user_id into our home activities.py code. Then setthe custom span to return a tracer value set for the user Id.  
![screenshots of the custom attribute](https://github.com/brahm0/aws-bootcamp-cruddur-2023/blob/9f262c82ba25085e61a2cf6f8fd19b7e1a1babb6/_docs/assets/Custom%20Attribute.png)![2](https://github.com/brahm0/aws-bootcamp-cruddur-2023/blob/9dd6dd1487db492765eae90b461d4af901322174/_docs/assets/Custom%20Attribute-%20User_id%20field.png)

