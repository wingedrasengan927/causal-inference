My notes and learnings from the books "Causal Inference in Python" by Matheus Facure and "Causal Inference for Data Science"

### Context

MIMIR is the insurance recommendation project I've worked on when I was at MMT.

My current project is to recommend add-ons when the user books a flight on the MakeMyTrip app. So when the user selects a flight, we recommend an add-on. An add-on can be an insurance. Now a third party insurance provider partners with us. They have many insurance plans. My job is to show the best plan to the user when they’re booking a flight. Now a plan has a certain price and benefits associated with it. The insurance company provides us with multiple plans. Note that we partner with multiple insurance providers and each of them have their own set of plans. My job is to suggest or recommend plans to the user so that the overall revenue is maximised. Now I cannot recommend the most pricy plan every time to every user, because if the user has less purchase power, then he may not select the add-on. So it makes sense to recommend a less pricy plan to a user with less purchase power.

My price plans (arms) are: `[79, 99, 129, 149, 199, 249, 349, 399, 449, 499]` (numbers have been altered)

We also have a deterministic policy in production that I want to beat. The deterministic policy is defined as follows:

```
def control_price_from_values(fare_per_pax):
    "Logic has been altered"
    fare = fare_per_pax
    if fare < 1000:
        return 79
    elif fare < 2000:
        return 99
    elif fare < 3000:
        return 129
    elif fare < 4000:
        return 149
    elif fare < 5000:
        return 199
    elif fare < 6000:
        return 249
    elif fare < 7000:
        return 349
    elif fare < 8000:
        return 399
    elif fare <= 10000:
        return 449
    else:
        return 499
```

Note that I have 5% pure exploration data as well