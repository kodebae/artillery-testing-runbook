# 📖 Artillery Testing Runbook

# API Resource
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

- In this test we've defined three distict phases:
1. Warm up the API - this phase will run for 60 seconds. Artillery will start by creating 5 new virtual users per second, and gradually ramp up to 10 new virtual users per second by the end of the phase.
2. Ramp up to peak load - this phase will also last for 60 seconds. Artillery will continue ramping up load from 10 to 50 virtual users per second.
3. Sustained peak load - this phase will run for 300 seconds. Artillery will create 50 new virtual users every second during this phase.



