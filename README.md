# 📖 Artillery Testing Runbook

## Getting started
| Install Artillery on your computer:

```
npm install -g artillery
```
## Resources
> Artillery is a modern, powerful & easy-to-use performance testing toolkit. Use it to ship scalable applications that stay performant & resilient under high load.

- You can use Artillery to run two types of performance tests:
Tests that put load on a system, i.e. load tests, stress tests, and soak tests
Tests that verify that a system is working as expected, i.e. continuous functional tests, also known by a number of other names such as: synthetic monitoring, semantic monitoring, production scripted testing, and continuous verification. Think ping on steroids - automated probes running continuously against services & APIs to test key user journeys.
- Artillery is typically used across teams responsible for delivery, testing, and operating production backend systems: from application developers, to test & QA engineers, and ops/SREs.

[Artillery docs:](https://www.artillery.io/docs)

## API Resource
```
curl http://asciiart.artillery.io:8080/dino
```
```
example output:

_. - ~ ~ ~ - .
   ..       __.    .-~               ~-.
   ((\     /   `}.~                     `.
    \\\   {     }               /     \   \
(\   \\~~^      }              |       }   \
 \`.-~ -@~      }  ,-.         |       )    \
 (___     ) _}   (    :        |    / /      `.
  `----._-~.     _\ \ |_       \   / /- _      `.
         ~~----~~  \ \| ~~--~~~(  + /     ~-.     ~- _
                   /  /         \  \          ~- . _ _~_-_.
                __/  /          _\  )
              .<___.'         .<___/
```

---

## Test script walkthrough

> Artillery test scripts have two parts: config and scenarios:
- config is what defines how our load test will run, e.g. the URL of the system we're testing, how much load will be generated, any plugins we want to use, and so on.
- scenarios is where we define what the virtual users created by Artillery will do. A scenario is usually a sequence of steps that describes a user session in the app.

- We set the target: ```target: http://asciiart.artillery.io:8080``` This means that all requests will use that base URL by default.

- Define load phases: We describe the load phases in the next section. Load phases tell Artillery how many virtual users to create, and describe the shape of the load we want.

- In this test we've defined three distinct phases:

1. Warm up the API - this phase will run for 60 seconds. Artillery will start by creating 5 new virtual users per second, and gradually ramp up to 10 new virtual users per second by the end of the phase.
2. Ramp up to peak load - this phase will also last for 60 seconds. Artillery will continue ramping up load from 10 to 50 virtual users per second.
3. Sustained peak load - this phase will run for 300 seconds. Artillery will create 50 new virtual users every second during this phase.

 | These phases will give us what's commonly known as a "spike test", where load on our API spikes to a high-level for a short amount of time. In the real world this may be the result of something like a newsletter going out, a flash sale, or an expected daily peak in usage of our app.

- Define scenarios: Our scenarios section defines one scenario. Each virtual user created in this test will run this scenario.

| The scenario contains three steps, each of which is a HTTP GET request to a different endpoint. We use the loop action to repeat those 3 requests 100 times.
Every virtual user running the scenario is completely independent of other virtual users running the same scenario, just like users and API clients in the real world. No memory, network connections, cookies, or other state is shared between virtual users.

## Running our load test
- to run the load tests, runt eh following command in your terminal window. 
```
artillery run asciiart-load-test.yml
```
> Artillery will run the test, launching new virtual users as defined by the config.phases spec. As virtual users run their scenario and collect performance metrics, Artillery will print a report every 10 seconds with a summary of collected metrics for that time period.

You will see your output in the terminal.

### 🥳 Congrats! You have just run your first load test with Artillery.


