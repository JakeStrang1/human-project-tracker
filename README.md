# Humanproject.info – the issue tracker
An API for generating a fictional human from Earth based on statistical data.

## Try it!

Go to [https://humanproject.info/human](https://humanproject.info/human).

## What is it...

Humanproject.info is an API that generates a statistically random human. When you go to [https://humanproject.info/human](https://humanproject.info/human), you'll get a payload that contains the attributes of a new random human. Right now the only attributes are `data.nationality` and `data.gender`. You can also see meta information for how these attributes were generated, like the probability of the result you received, the publicly-available dataset where this information comes from, and the [surprise index](#surprise-index).

I want this to be used primarily as a perspective tool. Right now our "human" is looking pretty sparse, but I hope we can add many more attributes to round them out like age, income, education, health situation, ethnicity, family, sexual identity, values, and especially, a name. We can try to get a picture of what our neighbours around the world might be like. We can pose questions: "How does my life situation compare to what I see represented in this data?", "How do the results change if I lock in a particular attribute like nationality or age?", "Who do I _not_ see represented in this data?"

Here's the result I just got (surprise index of 34, nice! 😄):
```
{
  "data": {
    "nationality": {
      "country_name": "Kyrgyz Republic",
      "country_code": "KGZ"
    },
    "gender": "female"
  },
  "meta": {
    "generator": [
      {
        "field": "nationality",
        "description": "Uniform random sample from 2022 World Bank population by country",
        "probability": 0.000879807100601038,
        "surprise_index": 34.1449927835944,
        "dependencies": [],
        "sources": [
          "https://data.worldbank.org/indicator/SP.POP.TOTL"
        ]
      },
      {
        "field": "gender",
        "description": "Either 'male' or 'female' using weighted sample from 2022 World Bank female population by country",
        "probability": 0.5090173276,
        "surprise_index": 1,
        "dependencies": [
          "nationality"
        ],
        "sources": [
          "https://genderdata.worldbank.org/indicators/sp-pop-totl-fe-zs?year=2022"
        ]
      }
    ]
  }
}
```

## Surprise Index

AKA, how cool is my result??

_If the surprise index is one million, then your result is literally 'one in a million ✨'._

The surprise index here corresponds to the likelihood of getting a result of _equal or lesser probability_ than your actual result. If your actual result has a surprise index of 20 then that means you had a 1 in _20_ chance of getting a result as rare or rarer than your actual result. Put differently, if we generate random humans over and over (an admittedly addicting pastime for nerds like me) and check their surprise index, we expect it to take on average 20 attempts to see a result with a surprise index as high as 20.

If your surprise index is 1, then you had a 1 in 1 (i.e. 100%) chance of getting a result as rare or rarer than your actual result. AKA, you got the most common result.

## Progress
_See what's next on the roadmap and how we got here_

### Iteration 3
**Status:** Roadmapped

GET /human
```
{
    "data": {
        "nationality": {
            "country_name": "China",
            "country_code": "CHN"
        },
        "gender": "female",
        "age": 35
    },
    "meta": {
        "generator": [
            {
                "field": "nationality",
                "description": "Uniform random sample from 2022 World Bank population by country"
                "probability": 0.178
                "sources": []
            },
            {
                "field": "gender",
                "description": "Either male or female by weighted sample from 2022 World Bank female population by country"
                "probability": 0.48969,
                "dependencies": ["nationality"]
                "sources": []
            },
            {
                "field": "age",
                "description": ""
                "probability": 0.035,
                "dependencies": ["nationality", "gender"]
                "sources": []
            },
        ]
    }
}
```

### Iteration 2
**Status:** Released

GET /human
```
{
    "data": {
        "nationality": {
            "country_name": "China",
            "country_code": "CHN"
        },
        "gender": "female"
    },
    "meta": {
        "generator": [
            {
                "field": "nationality",
                "description": "Uniform random sample from 2022 World Bank population by country"
                "probability": 0.178
                "sources": []
            },
            {
                "field": "gender",
                "description": "Either male or female by weighted sample from 2022 World Bank female population by country"
                "probability": 0.48969,
                "dependencies": ["nationality"]
                "sources": []
            },
        ]
    }
}
```

### Iteration 1
**Status:** Released

GET /human
```
{
    "data": {
        "nationality": {
            "country_name": "China",
            "country_code": "CHN"
        }
    },
    "meta": {
        "generator": [
            {
                "field": "nationality",
                "description": "Uniform random sample from 2022 World Bank population by country"
                "probability": 0.178
                "sources": []
            }
        ]
    }
}
```
