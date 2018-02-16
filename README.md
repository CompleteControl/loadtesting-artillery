<p align="center"><a href="https://artillery.io"><img src="https://artillery.io/img/flag.png" height="55" /></a></p>
<p align="center"><em><strong>Artillery</strong> is a modern, powerful, easy-to-use load-testing toolkit.</em> Artillery has a strong focus on developer happiness &amp; ease of use, and a batteries-included philosophy. Our goal is to help developers build <strong>faster</strong>, more <strong>resilient</strong> and more <strong>scalable</strong> applications.</p>

## Getting Started

Once Node.js is installed, install Artillery with:
```
npm install -g artillery
```
To check that the installation succeeded, run:
```
artillery -V
```

## Updating Artillery
```
npm install -g artillery@latest
```

## Run a quick test

Artillery has a quick command which allows you to use it for ad-hoc testing (in a manner similar to ab). Run:

```
artillery quick --count 10 -n 20 https://artillery.io/
```

This command will create 10 "virtual users" each of which will send 20 HTTP GET requests to https://artillery.io/.

## Run a test script

While the quick command can be useful for very simple tests, the full power of Artillery lies in being able to simulate realistic user behavior with scenarios. Let’s see how we’d run one of those.

```
{
  "config": {
    "target": "https://artillery.io",
    "phases": [
      {
        "duration": 60,
        "arrivalRate": 1
      }
    ],
    "defaults": {
      "headers": {
        "x-my-service-auth": "987401838271002188298567"
      }
    }
  },
  "scenarios": [
    {
      "flow": [
        {
          "get": {
            "url": "/docs/"
          }
        },
        {
          "get": {
            "url": "/docs/getting-started/"
          }
        },
        {
          "get": {
            "url": "/docs/basic-concepts/"
          }
        },
        {
          "get": {
            "url": "/docs/script-reference/"
          }
        },
        {
          "get": {
            "url": "/docs/http-reference/"
          }
        }
      ]
    }
  ]
}
```

## What our test does

In this script, we specify that we are testing a service running on https://artillery.io which will be talking to over HTTP. We define one load phase, which will last 60 seconds with 1 new virtual user (arriving every second (on average).

Then we define one possible scenario for every new virtual user to pick from, which consists of one GET request.

We also set an x-my-service-auth header to be sent with every request

## Running the test

Run the test with:

```
artillery run scripts/example.json
```