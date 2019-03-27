# MQTT.js answers to the survey

## What are the biggest problems your package need to face?

Internet of Things developers come to MQTT.js as one of their first interactions with
Node.js. Our users reports from generic Node.js questions e.g. what is
`client.on('message', fn)`, to MQTT protocol question e.g. what Quality
of Service should they use. They very often asks questions about
non-open source broker support. In the end, they _think_ this is a
*PAID*
support channel for the MQTT broker or device they *bought*.

All of this makes it incredibly hard to keep an healthy
issue tracker: at this point it has more than 100+ issues, with no plan
to address them.

Given that most of the users are not very much skilled in Node.js, it is
extremely hard to covert them to maintainers.

## What are the most time-consuming tasks?

1. anwswering issues, and I (@mcollina) have given up.
2. keep the tests green, as we adopted a wrong approach to testing for
   this module. Refactoring this would be a massive endeavour.
3. make sure that the changes proposed in PRs are actually
   spec-compliant.

## Which are the most difficult thing to implement in your package ecosystem? (ex: CI/CD, Versioned API Docs, etc...)

Keep the CI green across multiple Node.js versions. This is mainly due
to the nature of the module: there are a lot of timers and TCP
connections at play.

MQTT.js use Mocha for testing, and this has turned out to be a bad
choice for this module. Mocha runs all tests in a single Node.js
process: side effects with timers, reconnects, ports, etc, are extremely
hard to track down.

Better docs for people new to Node.js would be awesome.

## What do you think that is missing in your package ecosystem? (ex: CITGM, etc..)

I (@mcollina) have personal opinions, but none releated to this
specific module.

## What are the tasks that don't let you focus in the business code?

Issues handling.

## How is designed you process to add new maintainers in your package?

We follow Open Open Source. However very few people stick around.

## What type of automation could help you?

None really.

## What are the most frequent problems?

I do not understand the question.

## What would you like to do to us?

Help out in maintaining a good issue tracker. Help in growing a stable
community of maintainers.

## What problems are due to your dependencies?

None.

## Are your dependencies need of help?

Definitely. [websocket-stream](http://npm.im/websocket-stream)
likely needs a rewrite.

## Do you have to contribute to your dependencies? Do you establish a good communication channel?

Yes, I (@mcollina) inherited [websocket-stream](http://npm.im/websocket-stream).
